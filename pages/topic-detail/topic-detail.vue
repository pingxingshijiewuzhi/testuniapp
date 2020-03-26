<template>
	<view>
		<topic-info :item='topicInfo'></topic-info>
		<swiper-tab-header :tabBars='tabBars' :tabIndex='tabIndex'
		@tabIndexChange='tabIndexChange'
		scrollStyle='border-bottom:none'
		scrollItemStyle='width:50%'
		></swiper-tab-header>
		
		<!-- 列表 -->
		<view class='topic-detail-list'>
			<block v-for='(item,index) in tablist' :key='index'>
				<template v-if='tabIndex==index'>
					<!-- 列表 -->
					<block v-for='(it,ind) in  item.list' :key='ind'>
						<common-list :item='it' :index='ind'></common-list>
					</block>
				<!-- 上拉加载 -->
				<load-more :loadtext='item.loadtext'></load-more>
				</template>
			</block>
		</view>
	</view>
</template>

<script>
	import topicInfo from '../../components/topic/topic-info.vue'
	import swiperTabHeader  from '../../components/index/swiper-tab-header.vue'
	import commonList from "../../components/common/common-list.vue"
	import loadMore from '../../components/common/load-more.vue'
	export default {
		data() {
			return {
				tabIndex:0,
				tabBars:[
					{name:'默认',id:'moren'},
					{name:'最新',id:'zuixin'}
				],
				tablist:[
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
				topicInfo:{
					titlepic:'../../static/图片素材/datapic/15.jpg',
					title:'忆往事，警余生',
					desc:'我是描述',
					totalnum:100,
					todaynum:200
				}
			}
		},
		// 上拉触底
		onReachBottom(){
			// 上拉加载
		this.loadmore()
		},
		// 下拉刷新
		onPullDownRefresh(){
			this.getData()
		},
		methods: {
			tabIndexChange(index){
				this.tabIndex = index
			},
			// 获取数据
			getData(){
				// 获取数据
				// 赋值
				// 关闭下拉刷新
				setTimeout(()=> {
				            uni.stopPullDownRefresh();
				        }, 1000);
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
		},
		components:{
			topicInfo,
			swiperTabHeader,
			commonList,
			loadMore
		}
	}
</script>

<style>

</style>
