<template>
	<view>
		<!-- 背景图 + 用户基本信息 -->
		<user-space-head :userinfo='userinfo'></user-space-head>
		<!-- 统计 -->
		<view class='user-space-data'>
			<home-data :homedata='spacedata'></home-data>
		</view>
		<view style='height:20upx;background:#F4F4F4;'></view>
		<!-- tab导航 -->
		<swiper-tab-header :tabBars='tabBars' :tabIndex='tabIndex'
		@tabIndexChange='tabIndexChange'
		scrollStyle='border-bottom:none'
		scrollItemStyle='width:33.33%'
		></swiper-tab-header>
		

		
		<block v-for='(item,index) in tablist' :key='index'>
			<template v-if='tabIndex==0'>
				<!-- 主页 -->
				<user-space-userinfo :userinfo='userinfo'></user-space-userinfo>
			</template>
			<template v-else-if='tabIndex==index'>
				<!-- 列表 -->
				<block v-for='(it,ind) in  item.list' :key='ind'>
					<common-list :item='it' :index='ind'></common-list>
				</block>
			<!-- 上拉加载 -->
			<load-more :loadtext='item.loadtext'></load-more>
			</template>
		</block>
		
		<user-space-popup :status='status'
		 @hidepopup='hidetoglepopup'
		 @lahei='lahei'
		 @remark='remark'></user-space-popup>
	</view>
</template>

<script>
	import userSpaceHead from '../../components/user-space/user-space-head.vue'
	import homeData from '../../components/home/home-data.vue'
	import swiperTabHeader  from '../../components/index/swiper-tab-header.vue'
	import userSpaceUserinfo from '../../components/user-space/user-space-userinfo.vue'
	import commonList from '../../components/common/common-list.vue'
	import loadMore from '../../components/common/load-more.vue'
	import userSpacePopup from '../../components/user-space/user-space-popup.vue'
	export default {
		components:{
			userSpaceHead,
			homeData,
			swiperTabHeader,
			userSpaceUserinfo,
			commonList,
			loadMore,
			userSpacePopup
		},
		// 上拉触底
		onReachBottom(){
			// 上拉加载
		this.loadmore()
		},
		data() {
			return {
				status:false,
				userinfo:{
					bgimg:1,
					username:'昵称',
					userpic:'../../static/图片素材/demo5.jpg',
					sex:0,
					age:18,
					isattention:false,
					regtime:'2018-11-15',
					id:125,
					birthday:"1993-11-18",
					job:'IT',
					pickerText: '江苏-徐州-睢宁',
					emotion:"married"
				},
				spacedata:[
					{name:'获赞',num:'10k'},
					{name:'关注',num:11},
					{name:'粉丝',num:10}
				],
				tabIndex:0,
				tabBars:[
					{name:'主页',id:'mainpage'},
					{name:'糗事',id:'qiushi'},
					{name:'动态',id:'dynamic'}
				],
				tablist:[
					{},
					{
						loadtext:'上拉加载更多',
						list:[// 文字
						{
							userpic:'../../static/图片素材/userpic/12.jpg',
							username:'昵称',
							sex:0,//0代表男，1代表女
							age:25,
							isguanzhu:false,
							title:'我是标题',
							titlepic:'',
							share:false,
							video:false,
							path:"深圳 龙岗",
							commentnum:10,
							sharenum:10,
							goodnum:55
						},
						// 图文
						{
							userpic:'../../static/图片素材/userpic/12.jpg',
							username:'昵称',
							sex:0,//0代表男，1代表女
							age:25,
							isguanzhu:false,
							title:'我是标题',
							titlepic:'../../static/图片素材/datapic/11.jpg',
							share:false,
							video:false,
							path:"深圳 龙岗",
							commentnum:10,
							sharenum:10,
							goodnum:55
						}]
					},
					{
						loadtext:'上拉加载更多',
						list:[// 文字
						{
							userpic:'../../static/图片素材/userpic/12.jpg',
							username:'昵称',
							sex:0,//0代表男，1代表女
							age:25,
							isguanzhu:false,
							title:'我是标题',
							titlepic:'',
							share:false,
							video:false,
							path:"深圳 龙岗",
							commentnum:10,
							sharenum:10,
							goodnum:55
						},
						// 图文
						{
							userpic:'../../static/图片素材/userpic/12.jpg',
							username:'昵称',
							sex:0,//0代表男，1代表女
							age:25,
							isguanzhu:false,
							title:'我是标题',
							titlepic:'../../static/图片素材/datapic/11.jpg',
							share:false,
							video:false,
							path:"深圳 龙岗",
							commentnum:10,
							sharenum:10,
							goodnum:55
						}]
					}
				],
			}
		},
		onNavigationBarButtonTap(e){
			if(e.index==0){
				this.hidetoglepopup()
			}
		},
		methods: {
			// 操作菜单显示隐藏
			hidetoglepopup(){
				this.status = !this.status
			},
			// 拉黑
			lahei(){
				console.log('拉黑')
				this.hidetoglepopup()
			},
			// 备注
			remark(){
				console.log('备注')
				this.hidetoglepopup()
			},
			tabIndexChange(index){
				this.tabIndex = index
			},
			loadmore(){
				if(this.tablist[this.tabIndex].loadtext != '上拉加载更多'){return}
								this.tablist[this.tabIndex].loadtext = '加载中'
								setTimeout(()=>{
									let obj={
									userpic:'../../static/图片素材/userpic/12.jpg',
									username:'昵称',
									sex:0,//0代表男，1代表女
									age:25,
									isguanzhu:false,
									title:'我是标题',
									titlepic:'../../static/图片素材/datapic/11.jpg',
									share:false,
									video:false,
									path:"深圳 龙岗",
									commentnum:10,
									sharenum:10,
									goodnum:55
									}
									this.tablist[this.tabIndex].list.push(obj)
									this.tablist[this.tabIndex].loadtext = '上拉加载更多'
								},1000)
			}
		}
	}
</script>

<style>
.user-space-margin{
	margin:15upx 0;
}
.user-space-data{
	background-color: #FFFFFF;
	position:relative;
	z-index:3;
	/* 还可以这样定义边框啊 */
	border-top-right-radius: 20upx;
	border-top-left-radius:20upx;
	margin-top:-15upx;
}
	

</style>
