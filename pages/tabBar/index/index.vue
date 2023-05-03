<template>
	<view class="content">
		<!-- <view class="text-area">
			<text class="title">{{title}}</text>
		</view> -->
		<!-- 轮播图 -->
		<view class="banner">
			<swiper :indicator-dots="true" circular="true" :autoplay="true" :interval="3000" :duration="1000">
				<swiper-item v-for="item in banner" :key="item.goods_id">
					<image :src="item.image_src" mode="aspectFit"></image>
				</swiper-item>
			</swiper>
		</view>
		<!-- 导航 -->
		<view class="nav">
			<view class="nav_item" v-for="(item,index) in nav" :key="index" @click="checkJump(item.name)" >
				<!-- <view class=""> -->
					<image :src="item.image_src" mode="aspectFit"></image>
				<!-- </view> -->
				<!-- <text>{{item.name}}</text> -->
			</view>
		</view>
		<!-- 热门商品 -->
		<view class="hotgoods">
			<view class="goods_item" v-for="(item,index) in hotgoods">
				<view class="goods_title">
					<text>{{item.floor_title.name}}</text>
					<!-- <image :src="item.floor_title.image_src" mode=""></image> -->
				</view>
				<view class="goods_product" v-for="i in item.product_list">
					<image :src="i.image_src" mode="aspectFill" @click="previewGoods(i)"></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// title: 'Hello',
				// 轮播图
				banner: [],
				// 导航栏
				nav:[],
				// 热门商品信息
				hotgoods:[]
			}
		},
		onLoad() {
			this.getBanner();
			this.getNav();
			this.getHotgoods();
		},
		// watch:{
			
		// },
		methods: {
			// 获取轮播图信息
			async getBanner(){
				 uni.request({
					url:"https://api-hmugo-web.itheima.net/api/public/v1/home/swiperdata",
					success:(res) => {
						this.banner=res.data.message
						// console.log(this.banner)
					}
				})
				
			},
			// 获取导航栏信息
			getNav(){
				uni.request({
					url:"https://api-hmugo-web.itheima.net/api/public/v1/home/catitems",
					success:(res)=>{
						this.nav=res.data.message
						// console.log(this.nav);
					}
				})
			},
			//获取热门商品 
			getHotgoods(){
				uni.request({
					url:"https://api-hmugo-web.itheima.net/api/public/v1/home/floordata",
					success:(res)=>{
						this.hotgoods=res.data.message
						// console.log(res.data)
					}
				})
			},
			// 点击图片到详情页面
			previewGoods(res){
				console.log(res)
				uni.navigateTo({
					url:"../../info/goodsInfo/goodsInfo?goods="+ encodeURIComponent(JSON.stringify(res)),
				})
			},
			checkJump(name){
				switch (name){
					case "分类":
						uni.navigateTo({
							url: '/pages/category/index/category'
						})
					break;
					case "秒杀拍":
						uni.navigateTo({
							url: '/pages/category/seckill/seckill'
						})
					break;
					case "超市购":
						uni.navigateTo({
							url: '/pages/category/supermarket/supermarket'
						})
					break;
					case "母婴品":
						uni.navigateTo({
							url: '/pages/category/maternal/maternal'
						})
					break;
					default:
					break;
				}
			},
		}
	}
</script>

<style lang="scss">
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
	/* #ifdef H5 */
	
	/* #endif */
	.banner{ 
		width: 100%;
		image{
			width: 100%;
			height: 100%;
		}
	}
	.nav{
		display:flex;
		flex-wrap: wrap;
		margin:10px auto;
		.nav_item{
			width:25%;
			text-align:center;
			image{
				width:200rpx;
				height:200rpx;
			}
		}
	}
	.hotgoods{
		.goods_item{
			.goods_title{
				image{
					height:100rpx;
					// width:1000rpx;
				}
				text{
					line-height:60px;
					font-size:32px;
					color:#55aaff;
				}
			}
			.goods_product{
				// width:50%;
				margin-bottom: 50rpx;
				padding: 5rpx;
				box-sizing: border-box;
				image{
					border-radius: 5px;
					// transition: transform 1s ease 0s;
					box-shadow:4px 5px 5px #888;
				}
			}
		}
	}
</style>
