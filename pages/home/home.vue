<template>
	<view>
		<template v-if='!isLogin'>
			<!-- 未登录 -->
			<view class='nologin'> 登录仿糗百科，体验更多功能</view>
			<!-- 第三方登录 -->
			<other-info></other-info>
			<!-- 账号密码登录 -->
			<view class='accountlogin' @tap='openlogin'>账号密码登录
				<view class='icon iconfont icon-jiuru'></view>
			</view>
		</template>
		<template v-else>	
			<!-- 登录 -->
			<home-info :homeinfo="homeinfo" ></home-info>
		</template>
		
		<!-- 数据 -->
		<home-data :homedata='homedata'></home-data>
		<!-- 广告位 -->
		<view class='home-nav'>
			<image src="../../static/图片素材/banner3.jpg" mode="widthFix"
			lazy-load ></image>
		</view>
		
		<!-- 功能列表 -->
		<view class='home-list' >
			<block v-for='(item,index) in  list' :key='index'>
				<home-list-item :item='item' :index='inedex'></home-list-item>
			</block>
			
		</view>
	</view>
</template>

<script>
import  homeListItem from '../../components/home/home-list-item.vue'
import homeInfo from '../../components/home/home-info.vue'
import otherInfo from '../../components/home/other-login.vue'
import homeData from '../../components/home/home-data.vue'
	export default {
		data() {
			return {
				isLogin:true,
				homedata:[
					{name:'糗事',num:0},
					{name:'动态',num:0},
					{name:'评论',num:0},
					{name:'收藏',num:0}
				],
				homeinfo:{
					userpic:'../../static/图片素材/userpic/16.jpg',
					username:'昵称',
					totalnum:0,
					todaynum:0
				},
				list:[
					{icon:'liulan',name:'浏览历史',clicktype:'',url:''},
					{icon:'huiyuanvip',name:'糗事认证',clicktype:'',url:''},
					{icon:'keyboard',name:'审核糗事',clicktype:'',url:''}
				]
			}
		},
		components:{
			homeListItem,
			homeInfo,
			otherInfo,
			homeData
		},
		methods: {
			openlogin(){
				uni.navigateTo({
					url:'../login/login'
				})
			}
		},
		onNavigationBarButtonTap(e){
			if(e.index==0){
				uni.navigateTo({
					url:'../user-set/user-set'
				})
			}
		}
	}
</script>

<style>
.nologin{
	display:flex;
	justify-content: center;
	padding:20upx 40upx;
}


.accountlogin{
	display:flex;
	justify-content: center;
}


.home-nav{
	padding:20upx;
}
.home-nav>image{
	border-radius:20upx;
	height:150upx;
}


.home-list{
	padding:20upx;
}

</style>
