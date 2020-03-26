<template>
	<view class='tag-sex icon iconfont'
	:class="[sex== '0' ? 'icon-nan':'icon-nv']">
		{{age}}
	</view>
</template>

<script>
	export default{
		props:{
			sex:Number,
			age:Number
		}
	}
</script>

<style scoped>
	.tag-sex{
		background-color: #007AFF;
		color:#FFFFFF;
		font-size:24upx;
		padding:4upx 10upx;
		margin-left:10upx;
		border-radius: 20upx;
		line-height: 20upx;
	}
	.icon-nv{
		background-color: #FF698D !important;
	}
</style>
