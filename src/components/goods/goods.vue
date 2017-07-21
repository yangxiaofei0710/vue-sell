<template>
	<div>
		<div class="goods">
			<div class="menu-wrapper" ref="menuwrapper">
				<ul>
					<li v-for="(item,index) in goods" class="menu-item" :class="{ 'current':currentIndex === index }" @click="selectMenu(index,$event)">
						<span class="text border-1px">
							<span v-show="item.type>0" class="icon" :class="classMap[item.type]"></span>
							{{ item.name }}
						</span>
					</li>
				</ul>
			</div>
			<div class="foods-wrapper" ref="foodwrapper">
				<ul>
					<li v-for="item in goods" class="food-list food-list-hook">
						<h1 class="title">{{item.name}}</h1>
						<ul>
							<li v-for="food in item.foods" class="food-item border-1px">
								<div class="icon">
									<img width="57px" height="57px" :src="food.icon">
								</div>
								<div class="content">
									<h2 class="name">{{food.name}}</h2>
									<p class="desc">{{food.description}}</p>
									<div class="extra">
										<span class="count">月售{{ food.sellCount }}份</span><span>好评率{{ food.rating }}%</span>
									</div>
									<div class="price">
										<span class="now">¥{{ food.price }}</span><span class="old" v-show="food.oldPrice">¥{{ food.oldPrice }}</span>
									</div>
								</div>
							</li>
						</ul>
					</li>
				</ul>
			</div>
		</div>
		<shopcart></shopcart>	
	</div>
</template>

<script>
import BScroll from 'better-scroll'
import shopcart from 'components/shopCart/shopCart'

const ERR_OK = 0
export default {
	components: {
		shopcart	
	},
	props:{
		seller: {
			type: Object
		}
	},
	data () {
		return {
			goods: [],
			listHeight: [],
			scrollY: 0
		}
	},
	computed: {
		currentIndex () {
			for(let i = 0; i < this.listHeight.length; i++){
				//判断当currentIndex在height1和height2之间的时候显示
				let height1 = this.listHeight[i]
				let height2 = this.listHeight[i + 1]
				 //最后一个区间没有height2
				if (!height2 || (this.scrollY >= height1 && this.scrollY < height2)) {
					return i
				}
			}
			return 0
		}
	},
	created () {
		this.classMap = ["decrease" , "discount" , "special" , "invoice" , "guarantee"]
		this.$http.get('/api/goods').then((res) => {
			if (res.data.errno === ERR_OK) {
          	this.goods = res.body.data
          	//dom结构加载结束
            this.$nextTick(() => {
                this._initScroll()
                this._calculateHeight()
            })
      		}
		})
	},
	methods:{
		selectMenu (index,event) {
        	if(!event._constructed){
        		return
        	}
        	let foodList = this.$refs.foodwrapper.getElementsByClassName('food-list-hook')
        	let el = foodList[index]
        	this.foodsScroll.scrollToElement(el,300)
        },
		_initScroll() {
            this.meunScroll = new BScroll(this.$refs.menuwrapper, {
            	click: true
            });
            this.foodsScroll = new BScroll(this.$refs.foodwrapper, {
            	//探针作用，实时监测滚动位置
            	probeType: 3
            });
            this.foodsScroll.on('scroll', (pos) => {
            	//scrollY接收变量
            	this.scrollY = Math.abs(Math.round(pos.y))
            })
        },
        _calculateHeight () {
        	let foodList = this.$refs.foodwrapper.getElementsByClassName('food-list-hook')
        	let height = 0
        	//把第一个高度送入数组
        	this.listHeight.push(height)
        	//通过循环foodList下的dom结构，将每一个li的高度依次送入数组
        	for (let i = 0; i < foodList.length; i++){
        		let item = foodList[i]
        		height += item.clientHeight
        		this.listHeight.push(height)
        	}
        },
        
	}
}
</script>

<style lang="less" rel="stylesheet/less" scoped>
@import "../../common/stylus/mixin.less";
.goods{
	display: flex;
	position: absolute;
	top: 162.27px;
	bottom: 46px;
	overflow: hidden;
	width: 100%;
	.menu-wrapper{
		flex: 0 0 80px;
		width: 80px;
		background: #f3f5f7;
		.menu-item{
			display: table;
			height: 54px;
			width: 56px;
			padding: 0 12px;
			line-height: 14px;
			&.current{
				position: relative;
				z-index: 10;
				margin-top: -1px;
				background: #fff;
				font-weight: 700;
				.text{
					.border-none();
				}
			}
			.icon{
				display: inline-block;
				vertical-align: top;
				height: 12px;
				width: 12px;
				margin-right: 2px;
				background-size: 12px 12px;
				background-repeat: no-repeat;
				&.decrease{
					.bg-image("../image/goods/decrease_3");
				}
				&.discount{
					.bg-image("../image/goods/discount_3");
				}
				&.guarantee{
					.bg-image("../image/goods/guarantee_3");
				}
				&.invoice{
					.bg-image("../image/goods/invoice_3");
				}
				&.special{
					.bg-image("../image/goods/special_3");
				}
			}
			.text{
				display: table-cell;
				width: 56px;
				vertical-align: middle;
				.border-1px(rgba(7,17,27,0.1));
				font-size: 12px;
				text-align: center;
			}
		}
	}
	.foods-wrapper{
		flex: 1;
		.title{
			padding-left: 14px;
			height: 26px;
			line-height: 26px;
			border-left: 2px solid #d9dde1;
			font-size: 12px;
			color: rgb(147, 153, 159);
			background: #f3f5f7;
		}
		.food-item{
			display: flex;
			margin: 18px;
			padding-bottom: 18px;
			.border-1px(rgba(7,17,27,0.1));
			&:last-child{
				.border-none;
				margin-bottom: 0;
			}
			.icon{
				flex: 0 0 57px;
				margin-right: 10px;
			}
			.content{
				flex: 1;
				.name{
					margin: 2px 0 8px 0;
					height: 14px;
					line-height: 14px;
					font-size: 14px;
					color: rgb(7, 17, 27);
				}
				.desc,.extra{
					line-height: 10px;
					font-size: 10px;
					color: rgb(147, 153, 159);
				}
				.desc{
					margin-bottom: 8px;
					line-height: 12px;
				}
				.extra{
					.count{
						margin-right: 12px;
					}
				}
				.price{
					font-weight: 700;
					line-height: 24px;
					.now{
						margin-right: 8px;
						font-size: 14px;
						color: rgb(240, 20, 20);
					}
					.old{
						text-decoration: line-through;
						font-size: 10px;
						color: rgb(147, 153, 159);
					}
				}
			}
		}
	}
}
	
</style>