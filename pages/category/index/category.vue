<!--  -->
<template>
	<!-- 商品分类 -->
	<view class="category">
			hello
	</view>
</template>

<script>
	export default {
		data() {
			return {
				category:[]
			}
		},
		onload:function(){
			console.log("option");
			// this.getCategory()
		},
		methods: {
			/* 获取信息 */
			getCategory(){
				// uni.request({
				// 	url:"https://api-hmugo-web.itheima.net/api/public/v1/categories",
				// 	success:(res)=>{
				// 		console.log(res);
				// 	}
				// })
			}
		}
	}
</script>

<style>

</style>
