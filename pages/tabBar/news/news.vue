<template>
	<view class="news">
		<view class="news-item" v-for="item in 8">
			<view class="news-img">
				<view class="news-pic">
					图片
				</view>
			</view>
			<view class="news-context">
				<view class="news-context-item">
					context
				</view>
				<view class="news-context-item">
					context
				</view>
				<view class="news-context-item">
					context
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	
</script>

<style lang="scss">
	.news-item{
		display: flex;
		justify-content: space-between;
		-webkit-justify-content: space-between;
		margin: 10rpx;
		padding: 10rpx;
		border: 1rpx solid #F0AD4E ;
		color: #777;
		.news-img{
			flex: 1;
			display: flex;
			justify-content: center;
			-webkit-justify-content:center;
			align-items: center;
			.news-pic{
				display: flex;
				width: 200rpx;
				height: 200rpx;
				background-color: #ebebeb;
				justify-content: center;
				-webkit-justify-content:center;
				align-items: center;
			}
		}
		.news-context{
			flex:2;
			display: flex;
			flex-direction: column;
			.news-context-item{
				display: flex;
				flex: 1;
				justify-content: center;
				-webkit-justify-content:center;
				background-color: #eee;
				margin: 10rpx;
			}
		}
	}
</style>
