<template>
	<view class="cart">
		<view class="">
			<view class="cart-item" v-if="goodslist.length!=0" v-for="(item,index) in goodslist">
				<view class="cart-top">
					<!-- 图片 -->
					<view class="cart-img">
						<image :src="item.imgUrl" mode="aspectFill"></image>
					</view>
					<!-- 商品名和单价 -->
					<view class="cart-right">
						<view class="cart-right-item cart-title">{{item.goodsTitle}}</view>
						<view class="cart-right-item cart-num">
							<view class="text" style="color: #ffaa7f;">单价：{{item.price}} &#165;</view>
							<view class="text">数量：{{item.goodsNumber}}</view>
						</view>
					</view>
				</view>
				<!-- 操作 -->
				<view class=" cart-but">
					<view class="text" style="color: #ffaa7f;">总价：{{item.sum}} &#165;</view>
					<view class="">
						<button type="warn" size="mini" @click="delGoods(index)">删除</button>
					</view>
				</view>
				
			</view>
		</view>
		<view v-if="goodslist.length!=0" class="cart-total">
			<view class="cart-total-item">
				总计：<text style="color: red;">{{total}}	&#165;</text>
			</view>
			<view class="cart-total-item">
				<button type="primary" size="mini" @click="settlement()">结算</button>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		onLoad(option) {
		},
		onShow() {
			uni.getStorage({
				key:"goods_list",
				success:(res)=>{
					this.goodslist=res.data
					// console.log(res.data)
				}
			})
		},
		data(){
			return{
				goodslist:[],//商品列表
			}
		},
		computed:{
			total(){
				let total=0;
				for (let item of this.goodslist) {
					total=total+item.sum
				}
				return total;
			}
		},
		methods:{
			// 删除指定商品
			delGoods(num){
				let mythis=this
				uni.showModal({
					title: '提示',
					// 提示文字
					content: '确认取消购买吗？',
					// 取消按钮的文字自定义
					cancelText: "取消",
					// 确认按钮的文字自定义
					confirmText: "确认",
					//删除字体的颜色
					confirmColor:'red',
					//取消字体的颜色
					cancelColor:'#000000',
					success: function(res) {
						if (res.confirm) {
								// 执行确认后的操作
							mythis.goodslist.splice(num,1)
							uni.setStorage({
								key : "goods_list",
								data:mythis.goodslist,
							})
						} 
						else {
								// 执行取消后的操作
						}
					}
				})
			},
			// 结算
			settlement(){
				uni.showModal({
					title:"提示",
					content: '确认购买吗？',
					cancelText: "取消",
					confirmText: "确认",
					confirmColor:'red',
					cancelColor:'#000000',
					success:(res)=>{
						if(res.confirm){
							this.goodslist=[]
							uni.removeStorage({
								key:"goods_list",
							})
						}
						
					}
				})
			}
		}
	}
</script>

<style lang="scss">
	.cart-item{
		display: flex;
		padding: 20rpx;
		// background-color: #eee;
		border-bottom: 2rpx solid #eeeeee;
		flex-direction: column;
		&:last-child{
			margin-bottom: 110rpx;
		}
		.cart-top{
			display: flex;
			margin-bottom: 10rpx;
			.cart-img{
				flex: 1;
				-webkit-flex: 1;
				width: 200rpx;
				height: 200rpx;
				-webkit-justify-content: center;
				justify-content: center;
				-webkit-align-items: center;
				align-items: center;
				image{
					width: 200rpx;
					height: 200rpx;
				}
			}
			.cart-right{
				padding: 10rpx;
				-webkit-flex: 3;
				flex: 3;
				text{
					height: 120rpx;
					text-align: left;
					padding-left: 20rpx;
					padding-top: 10rpx;
					margin: 10rpx;
				}
			.cart-num{
				display: flex;
				-webkit-flex: 1;
				flex: 1;
				margin: 10rpx;
				.text{
					flex: 1;
					-webkit-flex: 1;
				}
			}
		}
		
		}
	}
.cart-but{
	display: flex;
	align-items: center;
	-webkit-justify-content: space-between;
	justify-content: space-between;
	-webkit-flex: 1;
	flex: 1;
	border-top: 3rpx dashed #eee;
}
	.cart-right-item{
		padding: 10rpx;
		flex: 1;
		-webkit-flex: 1;
		height: 40%;
	}
	.cart-total{
		height: 100rpx;
		width: 100%;
		display: flex;
		position: fixed;
		border: 1rpx solid #eeeeee;
		bottom: 100rpx;
		background-color: #ffffff;
		left: 0rpx;
		-webkit-justify-content: space-between;
		justify-content: space-between;
		align-items: center;
		.cart-total-item{
			margin: 15rpx;
			// flex: 1;
			// -webkit-flex:1;
		}
	}
</style>
