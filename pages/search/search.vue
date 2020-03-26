<template>
	<view>
		<template v-if='list.length>0'>
			<block v-for='(item,index) in  list' :key='index'>
			<Index-list :item='item' :index='index'></Index-list>
			</block>
			<load-more :loadtext='loadtext'></load-more>
		</template>
		<template v-else-if='issearch && list.length<1'>
			<!-- 无内容默认 -->
			<no-thing></no-thing>
		</template>
	</view>
</template>

<script>
	import IndexList from '../../components/index/index-list.vue'
	import noThing from '../../components/common/nothing.vue'
	import loadMore from '../../components/common/load-more.vue'
	export default {
		components:{
			IndexList,
			noThing,
			loadMore
		},
		data() {
			return {
				issearch:false,
				loadtext:"上拉加载更多",
				list:[],
				searchtext:''
			}
		},
		// 监听原生标题栏按钮点击事件(页面生命周期)
		onNavigationBarButtonTap(e){
			// console.log(JSON.stringify(e))
			// console.log(e.index)
			if(e.index == 0){
			uni.navigateBack({
			    delta: 1
			});	
			}
		},
		onNavigationBarSearchInputChanged(e){
			// console.log(JSON.stringify(e.text))
			// this.issearch= true
			this.serachtext = e.text
			// e.text && this.getdata(e.text)
		},
		// 监听原生标题栏搜索输入框搜索事件，用户点击软键盘上的“搜索”按钮时触发
		onNavigationBarSearchInputConfirmed(e){
			this.issearch= true
			e.text && this.getdata()
		},
		// 监听页面触底事件
		onReachBottom(){
			this.loadmore()
		},
		// 下拉刷新
		onPullDownRefresh(){
			this.getdata()
			// 停止下拉刷新
			uni.stopPullDownRefresh()
		},
		methods: {
			// 搜索事件
			getdata(){
				// 请求服务器
				uni.showLoading()
				setTimeout(()=>{
					let arr = [
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
					this.list = arr
					uni.hideLoading()
				},1000)
			},
			loadmore(){
				if(this.loadtext != '上拉加载更多'){return}
				this.loadtext = '加载中'
				setTimeout(()=>{
					let obj={
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
					}
					this.list.push(obj)
					this.loadtext = '上拉加载更多'
				},1000)
				// this.loadtext = '没有更多数据了'
			}
			
		}
	}
</script>

<style>

</style>
