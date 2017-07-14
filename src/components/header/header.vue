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
					{{ seller.description }}/{{ seller.deliveryTime }}分钟送达
				</div>
				<div v-if="seller.supports" class="support">
					<span class="icon"></span>
					<span class="text">{{ seller.supports[0].description }}</span>
				</div>
			</div>
		</div>
		<div class="bulletin-wrapper">
			
		</div>
	</div>
</template>

<script>
export default {
	props: {
		seller: {
			type: Object
		}
	}
}
</script>

<style lang="less" rel="stylesheet/less" scoped>
.avatar img{
	width: 4.26rem;
}
@picUrl: 'brand';
.header{
	color: #fff;
	background: #000;
	.content-wrapper{
		padding: 24px 12px 18px 24px;
		font-size: 0;
		.avatar{
			display: inline-block;
		}
		.content{
			display: inline-block;
			margin-left: 1rem;
			font-size: 1rem;
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
					line-height: 100%;
					font-weight: bold;
				}
			}
		}
	}
}
</style>
