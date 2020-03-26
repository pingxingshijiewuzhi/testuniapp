<template>
	<view>
		<detail-info :item='detail'></detail-info>
		<view class="u-comment-title">最新评论{{comment.count}}</view>
		<view class='uni-comment u-comment'>
			<block v-for='(item,index) in  comment.list' :key='index'> 
					<comment-list :item='item' :index='index'></comment-list>
			</block>
			
			<!-- <view class="uni-comment-list u-comment-list-child" >
				<view class="uni-comment-face">
					<image  src="../../static/图片素材/banner2.jpg" mode="widthFix"></image>
				</view>
				<view class="uni-comment-body" >
					<view class="uni-comment-top"><text>小猫咪</text>
					</view>
					<view class="uni-comment-content">支持国产，什么鬼</view>
					<view class="uni-comment-date">
						<view>2天前</view>
					</view>
				</view>
			</view> -->
			
		</view>
		<!-- 在这里占位符，占据和输入框一样高度 -->
		<view style='height:120upx'></view>
		<!-- 输入框 -->
		<user-chat-bottom @submit='submit'></user-chat-bottom>
		
		<!-- 分享 -->
		<more-share :show='shareshow' @showShare='showShare'></more-share>
	<!-- 	<view class='more-share-model' v-if='shareshow' @tap='showShare'></view>
		<view class='more-share' v-if='shareshow'>
			<view class='more-share-title'>分享到</view>
			<scroll-view scroll-x class='more-share-body'>
				<view class='more-share-body-item' hover-class='more-share-body-hover'>
					<view class='icon iconfont icon-weixin more-share-wx'></view>
					<view>微信</view>
				</view>
				<view class='more-share-body-item' hover-class='more-share-body-hover'>
					<view class='icon iconfont icon-weixin more-share-pyq'></view>
					<view>微信朋友圈</view>
				</view>
				<view class='more-share-body-item' hover-class='more-share-body-hover'>
					<view class='icon iconfont icon-xinlangweibo more-share-wb'></view>
					<view>新浪微博</view>
				</view>
				<view class='more-share-body-item' hover-class='more-share-body-hover'>
					<view class='icon iconfont icon-QQ more-share-qq'></view>
					<view>QQ好友</view>
				</view>
				<view class='more-share-body-item' hover-class='more-share-body-hover'>
					<view class='icon iconfont icon-QQ more-share-qq'></view>
					<view>其他</view>
				</view>
			</scroll-view>
			<view class='more-share-bottom' hover-class='more-share-body-hover'
			@tap='showShare'>取消</view>
		</view> -->
	</view>
</template>

<script>
	import detailInfo from '../../components/detail/detail-info.vue'
	import time from '../../common/time.js'
	import commentList from '../../components/detail/comment-list.vue'
	import userChatBottom from '../../components/user-chat/user-chat-bottom.vue'
	import moreShare from '../../components/common/more-share.vue'
	export default {
		components:{
			detailInfo,
			commentList,
			userChatBottom,
			moreShare
		},
		data() {
			return {
				shareshow:false,
				comment:{
					count:20,
					list:[
					]		
				},
				detail:{
					userpic:'../../static/图片素材/userpic/12.jpg',
					username:'昵称',
					sex:0,//0代表男，1代表女
					age:25,
					isguanzhu:false,
					title:'我是标题',
					titlepic:'../../static/图片素材/datapic/11.jpg',
					morepic:['../../static/图片素材/datapic/11.jpg','../../static/图片素材/datapic/12.jpg',
					'../../static/图片素材/datapic/13.jpg','../../static/图片素材/datapic/14.jpg'],
					share:false,
					video:false,
					path:"深圳 龙岗",
					commentnum:10,
					sharenum:10,
					goodnum:55
				}
			}
		},
		methods: {
			// 初始化对象
			initdata(obj){
				uni.setNavigationBarTitle({
					// 修改窗口标题
				    title: obj.title
				});
			},
			// 获取评论
			getcomment(){
				let arr = [
						{
							// 一级评论
						id:1,
						fid:0,
						userpic:'../../static/图片素材/banner2.jpg',
						username:'小猫咪',
						time:'1554970014',
						data:'支持股从昂贵'
						},
						{
							id:2,
							fid:1,
							userpic:'../../static/图片素材/banner2.jpg',
							username:'小猫咪',
							time:'1554970014',
							data:'支持股从昂贵'
						},
						{
							id:3,
							fid:1,
							userpic:'../../static/图片素材/banner2.jpg',
							username:'小猫咪',
							time:'1554970014',
							data:'支持股从昂贵'
						},
						{
						id:4,
						fid:0,
						userpic:'../../static/图片素材/banner2.jpg',
						username:'小猫咪',
						time:'1554970014',
						data:'支持股从昂贵'
						}
				]
				for(let i =0 ; i<arr.length;i++){
				arr[i].time=time.gettime.gettime(arr[i].time)
				}
				this.comment.list = arr
			},
			submit(data){
				let obj = {
					id:1,
					fid:0,
					userpic:'../../static/图片素材/banner2.jpg',
					username:'小猫咪',
					time:time.gettime.gettime(new Date().getTime()),
					data:data
				}
				this.comment.list.push(obj)
				console.log(data)
			},
			// 显示分享
			showShare(){
				this.shareshow = !this.shareshow
			}
		},
		onLoad(e){
			// console.log(e.detailData)
			// 把字符串转化成对象
			this.initdata(JSON.parse(e.detailData))
			this.getcomment()
		},
		// 监听导航按钮
		onNavigationBarButtonTap(){
			if(e.index == 0){
			this.showShare()
			}
		}
	}
</script>

<style>
.u-comment{
	padding:0 20upx;
}
.u-comment-title{
		padding: 20upx;
		font-size: 30upx;
		font-weight: bold;
	}
</style>
