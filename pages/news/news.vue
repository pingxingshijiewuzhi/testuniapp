<template>
	<view>
		<!-- 自定义导航栏 -->
		<news-nav-bar @change-tabbar='changeTabbar'
		:tabIndex='tabIndex'
		:tabBars='tabBars'
		></news-nav-bar>
		<view class='uni-tab-bar'>
			<swiper class="swiper-box" 
			:style="{'height':swiperheight+'px'}"
			 :current="tabIndex"
			 @change='changeTab'>
				<swiper-item  class="swiper-item">
					<scroll-view scroll-y  class='list' @scrolltolower='loadmore'>
	<!-- 列表 -->
						<block v-for='(item,index) in  newlistobj.list' :key='index'>
											<common-list :item='item' :index='index'></common-list>
						</block>
						<!-- 上拉加载更多 -->
						<load-more :loadtext='newlistobj.loadtext'></load-more>
					</scroll-view>
				</swiper-item>
				<swiper-item  class="swiper-item">
					<scroll-view scroll-y  class='list'>
						<!-- 搜索框 -->
						<view class='search-input'>
						<input  class='uni-input'   placeholder="搜索内容"
						placeholder-class='icon iconfont icon-sousuo input-placeholder' />
						</view>
						<!-- 轮播图 -->
						<swiper :indicator-dots="true" :autoplay="true" class='topic-swiper'
						:interval="3000" :duration="1000" :circular="true">
						<block v-for='(item,index) in topic.swiper' :key='index'>
							<swiper-item>
								<image :src="item.src"
								 mode="widthFix"
								 lazy-load></image>
							</swiper-item>
						</block>
						</swiper>
						<!-- 热门分类 -->
						<news-topic-nav :nav='topic.nav'></news-topic-nav>
						<!-- 最近更新 -->
						<view class='topic-new'>
							<view>最近更新</view>
							<block v-for='(item,index) in topic.list' :key='index'>
								<new-topic-list :item='item' :index='index'></new-topic-list>
							</block>
						</view>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
		
	</view>
</template>

<script>
	import commonList from "../../components/common/common-list.vue"
	import loadMore from '../../components/common/load-more.vue'
	
	import newsNavBar from '../../components/news/news-nav-bar.vue'
	import newsTopicNav from '../../components/news/news-topic-nav.vue'
	import newTopicList from '../../components/news/news-topic-list.vue'
	
	export default {
		data() {
			return {
				swiperheight:500,
				tabIndex:0,
				tabBars:[
					{name:'关注',id:'guanzhu'},
					{name:'话题',id:'huati'}
				],
				newlistobj:{
					loadtext:'上拉加载更多',
					list:[
						// 文字
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
						},
						// 视频
						{
							userpic:'../../static/图片素材/userpic/12.jpg',
							username:'昵称',
							sex:0,
							age:25,
							isguanzhu:false,
							title:'我是标题',
							titlepic:'../../static/图片素材/datapic/11.jpg',
							share:false,
							video:{
								looknum:"20W",
								long:"2:47"
							},
							path:"深圳 龙岗",
							commentnum:10,
							sharenum:10,
							goodnum:55
						},
						// 分享
						{
							userpic:'../../static/图片素材/userpic/12.jpg',
							username:'昵称',
							sex:0,
							age:25,
							isguanzhu:false,
							title:'我是标题',
							titlepic:'',
							share:{
								title:"我是分享标题",
								titlepic:'../../static/图片素材/datapic/24.jpg'
							},
							video:false,
							path:"深圳 龙岗",
							commentnum:10,
							sharenum:10,
							goodnum:55
						}
					]
				},
				topic:{
					swiper:[
						{src:'../../static/图片素材/banner1.jpg'},
						{src:'../../static/图片素材/banner2.jpg'},
						{src:'../../static/图片素材/banner3.jpg'}
					],
					nav:[
						{name:'最新'},
						{name:'游戏'},
						{name:'打卡'},
						{name:'情感'},
						{name:'故事'},
						{name:'喜爱'}
					],
					list:[
						{
							titlepic:'../../static/图片素材/topicpic/1.jpeg',
							title:'#话题名称#',
							desc:"我是话题描述",
							totalnum:10,
							todaynum:20
						},
						{
							titlepic:'../../static/图片素材/topicpic/1.jpeg',
							title:'#话题名称#',
							desc:"我是话题描述",
							totalnum:10,
							todaynum:20
						},
						{
							titlepic:'../../static/图片素材/topicpic/1.jpeg',
							title:'#话题名称#',
							desc:"我是话题描述",
							totalnum:10,
							todaynum:20
						},
						{
							titlepic:'../../static/图片素材/topicpic/1.jpeg',
							title:'#话题名称#',
							desc:"我是话题描述",
							totalnum:10,
							todaynum:20
						}
					]
				},
				
			}
		},
		// onShow(){
		// 	uni.getSystemInfo({
		// 		success(res){
		// 			console.log(res.windowHeight)
		// 		let height = res.windowHeight - uni.upx2px(100);
		// 		console.log(height)
		// 		console.log(this)
		// 		this.swiperheight = height
		// 		}
		// 	})
		// },
		methods: {
			changeTabbar(index){
				this.tabIndex = index
			},
			changeTab(event){
				console.log(event.detail.current)
				this.tabIndex=event.detail.current
			},
			loadmore(){
				if(this.newlistobj.loadtext != '上拉加载更多'){return}
				this.newlistobj.loadtext = '加载中'
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
					this.newlistobj.list.push(obj)
					this.newlistobj.loadtext = '上拉加载更多'
				},1000)
				// this.newList[index].loadtext = '没有更多数据了'
			}
		},
		components:{
			newsNavBar,
			commonList,
			loadMore,
			newsTopicNav,
			newTopicList
		}
	}
</script>

<style>
.search-input{
	padding:20upx;
}
.search-input>input{
	background-color: #F4F4F4;
	border-radius: 10upx;
}
.input-placeholder{
	font-size:26upx;
	display: flex;
	justify-content: center;
}

.topic-swiper{
	padding:0 20upx 20upx;
}
.topic-swiper image{
	width:100%;
	border-radius:10upx;
}

.topic-new{
	padding:20upx;
	}
.topic-new>view:first-child{
	padding-bottom:10upx;
	font-size: 28upx;
}

</style>
