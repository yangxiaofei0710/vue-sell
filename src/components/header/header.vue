<template>
	<div class="header">
		<div class="content-wrapper">
			<div class="avatar">
				<img :src="seller.avatar" alt="头像">
			</div>
			<div class="content">
				<div class="title">
					<span class="brand"></span>
					<span class="name">{{ seller.name }}</span>
				</div>
				<div class="description">
					{{ seller.description }}&nbsp;/&nbsp;{{ seller.deliveryTime }}分钟送达
				</div>
				<div v-if="seller.supports" class="support">
					<span class="icon" :class="classMap[seller.supports[0].type]"></span>
					<span class="text">{{ seller.supports[0].description }}</span>
				</div>
			</div>
			<div v-if="seller.supports" class="support-count" @click='showDetail'>
				<span class="count">{{ seller.supports.length }}个</span>
				<i class="iconfont icon-more"></i>
			</div>
		</div>
		<div class="bulletin-wrapper" @click='showDetail'>
			<span class="bulletin-title"></span><span class="bulletin-text">{{ seller.bulletin }}</span>
			<i class="iconfont icon-more"></i>
		</div>
		<div class="background">
			<img :src="seller.avatar" width="100%" height="100%">
		</div>
		<div v-show="datailShow" class="detail">
			<div class="detail-wrapper clearfix">
				<div class="detail-main">
					<p>{{ seller.bulletin }}</p>
					<p>{{ seller.bulletin }}</p>
					<p>{{ seller.bulletin }}</p>
				</div>
			</div>
			<div class="detail-close">
				<i class="iconfont icon-close"></i>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		seller: {
			type: Object
		}
	},
	created () {
		this.classMap = ["decrease" , "discount" , "special" , "invoice" , "guarantee"]
	},
	data () {
		return {
			datailShow: false,
		}
	},
	methods: {
		showDetail () {
			this.datailShow = true
		}
	}
}
</script>

<style lang="less" rel="stylesheet/less" scoped>
@import "../../common/stylus/mixin.less";

@picUrl: 'brand';
.header{
	position: relative;
	overflow: hidden;
	color: #fff;
	background: rgba(7, 17, 27, 0.5);
	.content-wrapper{
		position: relative;
		padding: 24px 12px 18px 24px;
		font-size: 0;
		.avatar{
			display: inline-block;
			vertical-align: top;
			img {
				width: 4.26rem;
				border-radius: 2px;
			}
		}
		.content{
			display: inline-block;
			margin-left: 1rem;
			.title{
				margin: 2px 0 8px 0;
				.brand{
					display: inline-block;
					vertical-align: top;
					width: 2rem;
					height: 1.2rem;
					background-image: url("@{picUrl}@2x.png");
					@media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3){
						background-image: url("@{picUrl}@3x.png");
					}
					background-size: 100% 100%;
					background-repeat: no-repeat;
				}
				.name{
					margin-left: 6px;
					font-size: 1rem;
					line-height: 1.2rem;
					font-weight: bold;
				}
			}
			.description{
				margin-bottom:  10px;
				line-height: 12px;
				font-size: 12px;
				font-weight: 200;
			}
			.support{
				.icon {
					display: inline-block;
					vertical-align: top;
					height: 12px;
					width: 12px;
					margin-right: 4px;
					background-size: 12px 12px;
					background-repeat: no-repeat;
					&.decrease{
						background-image: url("decrease_1@2x.png");
						@media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3){
							background-image: url("decrease_1@2x.png");
						}
					}
					&.discount{
						background-image: url("discount_1@2x.png");
						@media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3){
							background-image: url("discount_1@2x.png");
						}
					}
					&.guarantee{
						background-image: url("guarantee_1@2x.png");
						@media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3){
							background-image: url("guarantee_1@2x.png");
						}
					}
					&.invoice{
						background-image: url("invoice_1@2x.png");
						@media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3){
							background-image: url("invoice_1@2x.png");
						}
					}
					&.special{
						background-image: url("special_1@2x.png");
						@media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3){
							background-image: url("special_1@2x.png");
						}
					}
				}
				.text{
					line-height: 12px;
					font-size: 10px;
				}
			}
		}
		.support-count{
			position: absolute;
			right: 12px;
			bottom: 14px;
			padding: 0 8px;
			height: 24px;
			line-height: 24px;
			border-radius: 14px;
			background-color: rgba(0, 0, 0, 0.2);
			text-align: center;
			.count{
				font-size: 10px;
			}
			.icon-more{
				margin-left: 2px;
				line-height: 24px;
				font-size: 10px;
			}
		}
	}
	.bulletin-wrapper{
		position: relative;
		height: 28px;
		line-height: 28px;
		padding: 0 22px 0 12px;
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
		background: rgba(7, 17, 27, 0.2);
		.bulletin-title{
			display: inline-block;
			vertical-align: top;
			margin-top: 8px;
			width: 22px;
			height: 12px;
			background-image: url("bulletin@2x.png");
			@media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3){
				background-image: url("bulletin@3x.png");
			}
			background-size: 100% 100%;
			background-repeat: no-repeat;
		}
		.bulletin-text{
			vertical-align: top;
			margin: 0 4px; 
			font-size: 10px;
		}
		.icon-more{
			position: absolute;
			font-size: 10px;
			right: 12px;
		}
	}
	.background{
		position: absolute;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		z-index: -1;
		filter: blur(10px);
	}
	.detail{
		position: fixed;
		z-index: 100;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		overflow: auto;
		background: rgba(7, 17, 27, 0.8);
		.detail-wrapper{
			min-height: 100%;
			.detail-main{
				margin-top: 64px;
				padding-bottom: 64px; 
			}
		}
		.detail-close{
			position: relative;
			width: 32px;
			height: 32px;
			margin: -64px auto 0 auto;
			clear: both;
			font-size: 32px;
			text-align: center;
		}
	}
}
</style>
