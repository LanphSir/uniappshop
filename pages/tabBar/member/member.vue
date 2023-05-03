<template>
	<view class="member">
		<view class="user">
			<view class="user-head">
				<image src="../../../static/icon/head0.svg" mode=""></image>
				<button type="primary" size="default" @click="toLogin()">点击登录</button>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data(){
			return{
				
			}
		},
		methods:{
			toLogin(){
				uni.navigateTo({
					url:"../../login/login"
				})
			}
		}
	}
</script>

<style lang="scss">
	.user-head{
		display: flex;
		justify-content: space-around;
		-webkit-justify-content: space-around;
		-webkit-align-items: center;
		align-items: center;
		width: 100%;
		height: 350rpx;
		flex-direction: column;
		image{
			width: 200rpx;
			height: 200rpx;
			border: 4rpx groove #808080;
			border-radius: 50%;
		}
	}
</style>
