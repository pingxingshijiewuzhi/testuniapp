<template>
	<view>
		<swiper-tab-header :tabBars='tabBars' :tabIndex='tabIndex'
		@tabIndexChange='tabIndexChange'></swiper-tab-header>
		
		<view class='uni-tab-bar'>
			<swiper class="swiper-box" 
			:style="{'height':swiperheight+'px'}"
			 :current="tabIndex"
			 @change='changeTab'>
				<swiper-item  class="swiper-item" v-for='(items,index) in newList' :key='index'>
					<scroll-view scroll-y  class='list' @scrolltolower='loadmore(index)'>
						<template v-if='items.list.length>0'>
						<!-- 话题列表 -->
						<view class='topicview'>
						<block v-for='(item,ind) in items.list' :key='ind'>
							<new-topic-list :item='item' :index='ind'></new-topic-list>
						</block>
						</view>
						<!-- 上拉加载 -->
						<load-more :loadtext='items.loadtext'></load-more>
						</template>
						<template v-else>
						<!-- 无内容默认 -->
						<no-thing></no-thing>
						</template>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import swiperTabHeader  from '../../components/index/swiper-tab-header.vue'
	import noThing from '../../components/common/nothing.vue'
	import loadMore from '../../components/common/load-more.vue'
	import newTopicList from '../../components/news/news-topic-list.vue'
	export default {
		components:{
			swiperTabHeader,
			noThing,
			loadMore,
			newTopicList
		},
		data() {
			return {
				swiperheight:500,
				tabIndex:0,
				tabBars:[
					{name:'关注',id:'guanzhu'},
					{name:'推荐',id:'tuijian'},
					{name:'热点',id:'redian'},
					{name:'体育',id:'tiyu'},
					{name:'财经',id:'caijing'},
					{name:'娱乐',id:'yule'}
				],
				newList:[
					{
						loadtext:"上拉加载更多",
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
					{
						loadtext:"上拉加载更多",
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
					{
						loadtext:"上拉加载更多",
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
					{
						loadtext:"上拉加载更多",
						list:[]
					},
					{
						loadtext:"上拉加载更多",
						list:[]
					},
					{
						loadtext:"上拉加载更多",
						list:[]
					}
				]
			}
		},
		onShow(){
			uni.getSystemInfo({
				success(res){
					console.log(res.windowHeight)
				let height = res.windowHeight - uni.upx2px(100);
				console.log(height)
				console.log(this)
				this.swiperheight = height
				}
			})
		},
		methods: {
			tabIndexChange(index){
				this.tabIndex = index
			},
			// swiper滑动事件
			changeTab(event){
				console.log(event.detail.current)
				this.tabIndex=event.detail.current
			},
			loadmore(index){
				if(this.newList[index].loadtext != '上拉加载更多'){return}
				this.newList[index].loadtext = '加载中'
				setTimeout(()=>{
					let obj={
						titlepic:'../../static/图片素材/topicpic/1.jpeg',
						title:'#话题名称#',
						desc:"我是话题描述",
						totalnum:10,
						todaynum:20
						}
					this.newList[index].list.push(obj)
					this.newList[index].loadtext = '上拉加载更多'
				},1000)
				// this.newList[index].loadtext = '没有更多数据了'
			}
		}
	}
</script>

<style>
.topicview{
	pading:0 20upx;
}
</style>
