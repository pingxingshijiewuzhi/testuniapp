<template>
	<view class='user-space-userinfo'>
		<view class='user-space-userinfo-item'>
			<view>账号信息</view>
			<view>糗龄：{{getRegAge}}</view>
			<view>糗百ID:{{userinfo.id}}</view>
		</view>
		<view class='user-space-userinfo-item'>
			<view>个人信息</view>
			<view>星座：{{getConstellation}}</view>
			<view>工作：{{userinfo.job}}</view>
			<view>故乡:{{userinfo.pickerText}}</view>
			<view>情感:{{userinfo.emotion}}</view>
		</view>
	</view>
</template>

<script>
	import t from '../../common/time.js'
	export default{
		props:{
			userinfo:Object
		},
		computed:{
			getRegAge(){
				return t.gettime.sumAge(this.userinfo.regtime)
			},
			getConstellation(){
				return t.gettime.getHoroscope(this.userinfo.birthday)
			}
		}
	}
</script>

<style scoped>
/* 主页样式 */
.user-space-userinfo{
	padding:0 30upx;
}
.user-space-userinfo-item{
	padding:20upx 0;
	border-bottom:1upx solid #EEEEEE;
}
.user-space-userinfo-item>view{
	color:#AAAAAA;
}
.user-space-userinfo-item>view:first-child{
	color:#333333;
	font-size:35upx;
	padding:15upx 0;
}
</style>
