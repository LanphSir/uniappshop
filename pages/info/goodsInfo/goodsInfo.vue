<template>
	<view id="goodsInfo">
		<view class="goodsInfo-item goods-img">
			<image :src="imgUrl" mode="center" @click="previewImg(imgUrl)"></image>
		</view>
		<view class="goodsInfo-item goods-title">
			商品名：<text>{{goodsTitle}}</text>
		</view>
		<view class="goodsInfo-item goods-text">
			商品描述：<text>{{goodsText}} &#40;限购{{maxgoods}}件&#41;</text>
		</view>
		<view class="goodsInfo-item purchase">
			<view class="goods-price">
				单价: <text style="color: red;">{{price}} &#165;</text>
			</view>
			<view class="settle">
				<view class="settle-count">
					购买数量：
					<view class="settle-count-but">
						<button :disabled="goodsNumber==0" class="settle-but" type="primary" size="mini" @click="goodsNumber--">-</button>
						<text class="settle-text">{{goodsNumber}}</text> 
						<button :disabled="goodsNumber==maxgoods" class="settle-but" type="primary" size="mini" @click="goodsNumber++">+</button>
					</view>
				</view>
				<view class="settle-sum">
					 总计：<text class="sum-text">{{sum}} &#165;</text>
					<button type="primary" plain="true" size="mini" @click="goCart()">加入购物车</button>
				</view>
			</view>
		</view>
	</view>
	
</template>

<script>
	export default {
		onLoad(option) {
			const goods=JSON.parse(option.goods);
			this.imgUrl=goods.image_src;
			this.goodsTitle=goods.name;
		},
		data() {
			return {
				imgUrl:"../../../static/icon/cart-active.png",//商品图片
				goodsTitle:"xxxxxxx",//商品名
				goodsText:"xxxxxxxxxxxxxxxxxxxxx",//商品介绍
				price:80,//单价
				goodsNumber:0,//购买数量
				maxgoods:5,//最大购买数量
			}
		},
		computed:{
			sum(){
				return this.price*this.goodsNumber;
			}
		},
		methods: {
			previewImg(url){
				let urls=[]
				urls[0] =url
				uni.previewImage({
					urls:urls,
				})
			},
			goCart(){
				if(this.goodsNumber!=0){
						let goods=new Object();
						var goodslist=[];
						goods.imgUrl=this.imgUrl;
						goods.price=this.price;
						goods.goodsTitle=this.goodsTitle;
						goods.goodsNumber=this.goodsNumber;
						goods.sum=this.sum;
						// 获取购物车列表
						uni.getStorage({
							key:'goods_list',
							success: function(res) {
								goodslist=res.data;
							},
							fail:function(){
								console.log("获取购物车列表错误")
							}
						});
						// 如果购物车为空则创建购物车
						if(goodslist.length==0){
							goodslist.push(goods);
							uni.setStorage({
								key:'goods_list',
								data:goodslist,
								success:function(){
									uni.showToast({
										title:"商品已添加到购物车",
										icon:'success',
										duration:2000
									})
								}
							})
						}
						else{
							var isRepeat;
							// 查询是否重复添加商品
							for (let item of goodslist) {
								if(item.goodsTitle==this.goodsTitle){
									uni.showToast({
										icon:"none",
										title:"该商品已在购物车中，请勿重复添加",
										duration:2000
									})
									isRepeat=true;
									break;
								}
							}
							// 如果没有重复则添加到购物车中
							if(!isRepeat){
								goodslist.push(goods);
								uni.setStorage({
									key:'goods_list',
									data:goodslist,
									success:function(){
										uni.showToast({
											title:"商品已添加到购物车",
											icon:'success',
											duration:2000
										})
									}
									})
							}
						}
				}
				else{
					uni.showToast({
						title:"你还未选择商品",
						icon:'none',
						duration:2000
					})
				}
			}
		}
	}
</script>

<style lang="scss">
	.goodsInfo-item{
		padding: 10rpx;
		margin-top: 10rpx;
		line-height: 40rpx;
	}
	.goods-img{
		width: 100%;
		margin: 0rpx 10rpx;
		box-sizing: border-box;
	}
	.goods-img image{
		width: 90%;
	}
	.settle-count{
		display: flex;
		-webkit-flex: 1;
		flex: 1;
		/* height: 200rpx; */
		// -webkit-justify-content: center;
		// justify-content: center;
		-webkit-align-items: center;
		align-items: center;
		.settle-count-but{
			display: flex;
			align-items: center;
			.settle-text{
				border: 1rpx solid #C8C7CC;
			}
		}
	}
	.settle-text{
		padding: 0rpx 40rpx;
		font-size: 38rpx;
		display: inline-block;
	}
	.sum-text{
		color: #DD524D;
	}
	/* .settle-but{
		width: 60rpx;
		height: 50rpx;
		background-color: #007AFF;
	} */
	.settle-sum{
		position: fixed;
		bottom: 1rpx;
		right: 5rpx;
		display: flex;
		-webkit-justify-content:center;
		justify-content: center;
		-webkit-align-items:center;
		align-items: center;
		margin: 0rpx 10rpx;
	}
		.sum-text{
			margin-right:50rpx ;
		}
</style>
