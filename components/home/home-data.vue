<template>
	<view class='hone-data'>
		<block v-for='(item,index) in homedata' :key='index'>
		<view class='home-data-item'>
			<view>{{item.num}}</view> {{item.name}}
		</view>
		</block>
	</view>
</template>

<script>
	export default {
		props:{
			homedata:Array
		}
	}
</script>

<style scoped>
.hone-data{
	display: flex;
	align-items:center;
	text-align: center;
	padding:20upx 40upx;
}
.home-data-item{
	flex:1;
	flex-direction:column;
	color:#989898;
}
.home-data-item>view{
	color:#333333;
	font-size:32upx;
}
</style>
