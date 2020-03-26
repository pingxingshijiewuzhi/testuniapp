<template>
	<view class='nothing animated fadeIn'>
		<image src="../../static/common/nothing.png" mode="widthFix"></image>
	</view>
</template>

<script>
	export default {
		
	}
</script>

<style scoped>
	.nothing{
		display: flex;
		justify-content:center;
		align-items:center;
		background-color: #FFFFFF;
		position:absolute;
		left:0;
		right:0;
		top:0;
		bottom:0;
	}
	.nothing image{
		width:60%;
	}
</style>
