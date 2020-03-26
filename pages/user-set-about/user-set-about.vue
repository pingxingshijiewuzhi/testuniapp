<template>
	<view>
		<view class='user-set-about-t'>
			<image src="../../static/common/logo.png"
			 mode="widthFix" lazy-load></image>
			<view>version 1.0.0</view>
		</view>
		<block v-for='(item,index) in  list' :key='index'>
			<home-list-item :item='item' :index='inedex'></home-list-item>
		</block>
	</view>
</template>

<script>
	import  homeListItem from '../../components/home/home-list-item.vue'
	export default {
		data() {
			return {
				list:[
					{icon:'',name:'新版本检测',clicktype:'',url:''},
					{icon:'',name:'仿糗事百科用户协议',clicktype:'',url:''}
				]
			}
		},
		methods: {
			
		},
		components:{
			homeListItem
		}
	}
</script>

<style>
.user-set-about-t{
	padding:20upx 0;
	display:flex;
	justify-content:center;
	align-items:center;
	flex-direction:column;
}
.user-set-about-t>image{
	margin-top: 30upx;
	margin-bottom: 20upx;
	width:60%;
}
..user-set-about-t>view{
	color:#CCCCCC;
}
</style>
