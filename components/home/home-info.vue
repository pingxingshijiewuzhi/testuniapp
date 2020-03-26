<template>
	<view class='home-info' @tap='toUserSpace'>
		<image :src="homeinfo.userpic" mode='widthFix' lazy-load></image>
		<view class='u-f1'>
			<view>{{homeinfo.username}}</view>
			<view>总访客 {{homeinfo.totalnum}} 今日 {{homeinfo.todaynum}} </view>
		</view>
		<view class='icon iconfont icon-jiuru'></view>
	</view>
</template>

<script>
	export default{
		props:{
			homeinfo:Object,
			index:Number
		},
		methods:{
			toUserSpace(){
				uni.navigateTo({
					url:'../../pages/user-space/user-space'
				})
			}
		}
	}
</script>

<style scoped>
	.home-info{
	display: flex;
		padding: 20upx;
	}
	.home-info>image{
		flex-shrink:0;
		width:100upx;
		height:100upx;
		border-radius:100%;
		margin-right: 10upx;
	}
	.home-info>view:last-of-type{
		height:100%;
	}
	.u-f1{
		flex:1;
	}
	.u-f1>view:first-child{
		font-size:32upx;
	}
	.u-f1>view:last-child{
		color:#BBBBBB;
		}
</style>
