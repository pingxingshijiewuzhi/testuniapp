<template>
	<view>
		<!-- 功能列表 -->
		<view class='home-list' >
			<block v-for='(item,index) in  list' :key='index'>
				<home-list-item :item='item' :index='inedex'></home-list-item>
			</block>
			<button type='primary' class='user-set-btn'>退出登录</button>
		</view>
	</view>
</template>

<script>
	import  homeListItem from '../../components/home/home-list-item.vue'
	export default {
		data() {
			return {
				list:[
					{icon:'',name:'账号与安全',clicktype:'navigateTo',url:'../../pages/user-set-repassword/user-set-repassword'},
					{icon:'',name:'绑定邮箱',clicktype:'navigateTo',url:'../../pages/user-set-email/user-set-email'},
					{icon:'',name:'资料编辑',clicktype:'navigateTo',url:'../../pages/user-set-userinfo/user-set-userinfo'},
					{icon:'',name:'小纸条',clicktype:'navigateTo',url:''},
					{icon:'',name:'清楚缓存',clicktype:'clear',url:''},
					{icon:'',name:'意见反馈',clicktype:'navigateTo',url:'../../pages/user-set-help/user-set-help'},
					{icon:'',name:'关于糗白',clicktype:'navigateTo',url:'../../pages/user-set-about/user-set-about'},
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

<style scoped>
.home-list{
	padding:20upx;
}
.user-set-btn{
	width:100%;
	padding:20upx 0;
	color:#333333!important;
	background-color: #FFE933!important;
	border:0!important;
}
</style>
