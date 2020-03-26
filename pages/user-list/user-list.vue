<template>
	<view class='currentbody'>
		<!-- tab切换 -->
		<swiper-tab-header :tabBars='tabBars' :tabIndex='tabIndex'
		@tabIndexChange='tabIndexChange'
		scrollStyle='border-bottom:0;'
		scrollItemStyle='width:33%;'></swiper-tab-header>
		
		<!-- 好友列表 -->
		<!-- <block v-for='(item,index) in  list' :key='index'>	
			<user-list :item='item'></user-list>
		</block> -->
		
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
							<user-list :item='item' :index='ind'></user-list>
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
	</view>
</template>

<script>
	import loadMore from '../../components/common/load-more.vue'
	import swiperTabHeader  from '../../components/index/swiper-tab-header.vue'
	import userList from '../../components/user-list/user-list.vue'
	import noThing from '../../components/common/nothing.vue'
	export default {
		data() {
			return {
				swiperheight:500,
				tabIndex:0,
				tabBars:[
					{name:'互关',id:'huguan',num:12},
					{name:'关注',id:'guanzhu',num:22},
					{name:'粉丝',id:'fensi',num:44}
				],
				newList:[
					{
						loadtext:'上拉加载更多',
						list:[
							{
								userpic:'../../static/图片素材/userpic/12.jpg',
								username:'昵称',
								sex:0,//0代表男，1代表女
								age:25,
								isguanzhu:false
							},
							{
								userpic:'../../static/图片素材/userpic/12.jpg',
								username:'昵称',
								sex:1,//0代表男，1代表女
								age:18,
								isguanzhu:true
							},
							{
								userpic:'../../static/图片素材/userpic/12.jpg',
								username:'昵称',
								sex:1,//0代表男，1代表女
								age:58,
								isguanzhu:true
							}
						]
					},
					{
						loadtext:'上拉加载更多',
						list:[
							{
								userpic:'../../static/图片素材/userpic/12.jpg',
								username:'昵称',
								sex:0,//0代表男，1代表女
								age:25,
								isguanzhu:false
							},
							{
								userpic:'../../static/图片素材/userpic/12.jpg',
								username:'昵称',
								sex:1,//0代表男，1代表女
								age:18,
								isguanzhu:true
							}
						]
					},
					{
						loadtext:'上拉加载更多',
						list:[
							{
								userpic:'../../static/图片素材/userpic/12.jpg',
								username:'昵称',
								sex:0,//0代表男，1代表女
								age:25,
								isguanzhu:false
							},
							{
								userpic:'../../static/图片素材/userpic/12.jpg',
								username:'昵称',
								sex:1,//0代表男，1代表女
								age:18,
								isguanzhu:true
							}
						]
					}
				]
				
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
					userpic:'../../static/图片素材/userpic/12.jpg',
					username:'昵称',
					sex:0,//0代表男，1代表女
					age:25,
					isguanzhu:false
					}
					this.newList[index].list.push(obj)
					this.newList[index].loadtext = '上拉加载更多'
				},1000)
				// this.newList[index].loadtext = '没有更多数据了'
			}
		},
		onNavigationBarButtonTap(e){
			if(e.index==0){
				uni.navigateBack({
					delta:1
				})
			}
		},
		components:{
			swiperTabHeader,
			userList,
			loadMore,
			noThing
		}
	}
</script>

<style scoped>
.currentbody{
	padding:0 20upx;
}

</style>
