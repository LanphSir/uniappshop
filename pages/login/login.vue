<template>
	<view>
		<view class="login">
			<!-- 账号登录 -->
			<view class="login-form">
				<view class="login-input">
					<text>账号：</text> <input type="text" class="username" value="" placeholder="请输入账号/手机号" />
				</view>
				<view class="login-input">
					<text>密码：</text> <input type="text" class="password" value="" password="ture" />
				</view>
				
				<view class="login-but">
					<button type="primary" size="default">登录</button>
					<button type="primary" size="default">注册</button>
				</view>
			</view>
			<!-- 第三方登录 -->
			<view class="login-extra">
				<view class="login-extra-item">
					<image src="../../static/icon/wxlogo.svg" mode="widthFix"></image>
				</view>
				<view class="login-extra-item">
					<image src="../../static/icon/qqlogo.svg" mode="widthFix"></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style lang="scss">
	.login{
		display: flex;
		flex-direction: column;
		// justify-content: space-between;
		// -webkit-justify-content: space-between;
		height: 100vh;
		// -webkit-align-items: center;
		// align-items: center;
		.login-form{
			flex: 1;
			display: flex;
			justify-content: center;
			-webkit-justify-content: center;
			-webkit-align-items: center;
			align-items: center;
			flex-direction: column;
			width: 100%;
			.login-input{
				display: flex;
				-webkit-align-items: center;
				align-items: center;
				justify-content: center;
				-webkit-justify-content: center;
				input{
					line-height:60rpx;
					padding: 5rpx 10rpx;
					border: 1rpx solid #808080;
					height: 60rpx;
					// width: 400rpx;
					margin: 10rpx 0rpx;
					display: inline-block;
				}
			}
			.login-but{
				margin-top: 20rpx;
				width: 70%;
				display: flex;
				flex-direction: row;
				justify-content: center;
				-webkit-justify-content: center;
				-webkit-align-items: center;
				align-items: center;
			}
		}
		.login-extra{
			width: 100%;
			display: flex;
			flex: 1;
			height: 200rpx;
			justify-content: center;
			-webkit-justify-content: center;
			-webkit-align-items: center;
			align-items: center;
			.login-extra-item{
				display: flex;
				justify-content: center;
				-webkit-justify-content: center;
				flex: 1;
				image{
					width: 80rpx;
					height: 80rpx;
				}
				
			}
		}
	}
</style>
