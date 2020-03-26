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
					<!-- 图文列表 -->
					<block v-for='(item,ind) in items.list' :key='ind'>
						<index-list :item='item' :index='ind'></index-list>
					</block>
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
	<!-- <block v-for='(item,index) in list' :key='index'>
		<index-list :item='item' :index='index'></index-list>
	</block> -->
	
	<!-- 下面是先静态写出来的模板 -->
		<!-- <view class='index-list'>
			<view class='index-item1'>
				<view>
					<image src="../../static/图片素材/userpic/12.jpg" mode="widthFix" lazy-load></image>
					昵称
				</view>
				<view>
					<view class='icon iconfont icon-zengjia'></view>
					关注
				</view>
			</view>
			<view class='index-item2'>我是标题</view>
			<view class='index-item3'>
				<image src="../../static/图片素材/datapic/11.jpg" mode="widthFix" lazy-load></image>
				
				<view class='index-item-play icon iconfont icon-bofang'></view>
				<view class='index-item-playinfo'>
					20万次播放  2:47
				</view>
			</view>
			<view class='index-item4'>
				<view>
					<view><view class='icon iconfont icon-icon_xiaolian-mian'></view>10</view>
					<view><view class='icon iconfont icon-kulian'></view>20</view>
				</view>
				<view>
					<view><view class='icon iconfont icon-pinglun1'></view>20</view>
					<view><view class='icon iconfont icon-zhuanfa'></view>280</view>
				</view>
			</view>
		</view> -->
</view>

</template>

<script>
	import indexList from '../../components/index/index-list.vue'
	import swiperTabHeader  from '../../components/index/swiper-tab-header.vue'
	import loadMore from '../../components/common/load-more.vue'
	import noThing from '../../components/common/nothing.vue'
	export default {
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
								userpic:'../../static/图片素材/userpic/12.jpg',
								username:'昵称',
								isguanzhu:false,
								title:'我是标题',
								type:'img',//img:图文,video:视频
								titlepic:'../../static/图片素材/datapic/11.jpg',
								infonum:{
									index:0,//0:没有操作，1：顶2：踩
									dingnum:11,
									cainum:11
								},
								commentnum:10,
								sharenum:10
							},
							{
								userpic:'../../static/图片素材/userpic/12.jpg',
								username:'昵称',
								isguanzhu:false,
								title:'我是标题',
								type:'video',//img:图文,video:视频
								titlepic:'../../static/图片素材/datapic/11.jpg',
								playnum:'20w',
								long:'2:47',
								infonum:{
									index:2,//0:没有操作，1：顶2：踩
									dingnum:11,
									cainum:11
								},
								commentnum:10,
								sharenum:10
							}
						]
					},
					{
						loadtext:"上拉加载更多",
						list:[
							{
								userpic:'../../static/图片素材/userpic/12.jpg',
								username:'昵称',
								isguanzhu:false,
								title:'我是标题',
								type:'img',//img:图文,video:视频
								titlepic:'../../static/图片素材/datapic/11.jpg',
								infonum:{
									index:2,//0:没有操作，1：顶2：踩
									dingnum:11,
									cainum:11
								},
								commentnum:10,
								sharenum:10
							},
							{
								userpic:'../../static/图片素材/userpic/12.jpg',
								username:'昵称',
								isguanzhu:false,
								title:'我是标题',
								type:'video',//img:图文,video:视频
								titlepic:'../../static/图片素材/datapic/11.jpg',
								playnum:'20w',
								long:'2:47',
								infonum:{
									index:1,//0:没有操作，1：顶2：踩
									dingnum:11,
									cainum:11
								},
								commentnum:10,
								sharenum:10
							}
						]
					},
					{
						loadtext:"上拉加载更多",
						list:[
							{
								userpic:'../../static/图片素材/userpic/12.jpg',
								username:'昵称',
								isguanzhu:false,
								title:'我是标题',
								type:'img',//img:图文,video:视频
								titlepic:'../../static/图片素材/datapic/11.jpg',
								infonum:{
									index:1,//0:没有操作，1：顶2：踩
									dingnum:11,
									cainum:11
								},
								commentnum:10,
								sharenum:10
							},
							{
								userpic:'../../static/图片素材/userpic/12.jpg',
								username:'昵称',
								isguanzhu:false,
								title:'我是标题',
								type:'video',//img:图文,video:视频
								titlepic:'../../static/图片素材/datapic/11.jpg',
								playnum:'20w',
								long:'2:47',
								infonum:{
									index:0,//0:没有操作，1：顶2：踩
									dingnum:11,
									cainum:11
								},
								commentnum:10,
								sharenum:10
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
		onLoad() {

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
		// 监听搜索框点击事件
		onNavigationBarSearchInputClicked(){
			uni.navigateTo({
				url:'../search/search'
			})
		},
		// 监听原生标题栏按钮点击事件(页面生命周期)
		onNavigationBarButtonTap(e){
			switch(e.index){
				case 1:
				// 打开发布页面
				uni.navigateTo({
					url:'../add-input/add-input'
				})
				break
			}
		},
		methods: {
			// swiper滑动事件
			changeTab(event){
				console.log(event.detail.current)
				this.tabIndex=event.detail.current
			},
			tabIndexChange(index){
				this.tabIndex = index
			},
			loadmore(index){
				if(this.newList[index].loadtext != '上拉加载更多'){return}
				this.newList[index].loadtext = '加载中'
				setTimeout(()=>{
					let obj={
						userpic:'../../static/图片素材/userpic/12.jpg',
						username:'昵称',
						isguanzhu:true,
						title:'我是标题',
						type:'video',//img:图文,video:视频
						titlepic:'../../static/图片素材/datapic/11.jpg',
						playnum:'20w',
						long:'2:47',
						infonum:{
							index:2,//0:没有操作，1：顶2：踩
							dingnum:11,
							cainum:11
						},
						commentnum:10,
						sharenum:10
					}
					this.newList[index].list.push(obj)
					this.newList[index].loadtext = '上拉加载更多'
				},1000)
				// this.newList[index].loadtext = '没有更多数据了'
			}
		},
		components:{
			indexList,
			swiperTabHeader,
			loadMore,
			noThing
		}
	}
</script>

<style>

</style>
