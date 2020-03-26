<template>
	<view>
		<scroll-view scroll-y  id='scrollview'
		:scroll-top='scrollTop'
		:scroll-with-animation='true'
		:style="{height:style.contentH+'px'}">
		<!-- 聊天列表 -->
		<block v-for='(item,index) in  list' :key='index'>
			<user-chat-list :item='item' :index='index'></user-chat-list>
		</block>
		</scroll-view>
		<!-- 输入框 -->
	<user-chat-bottom @submit='submit'></user-chat-bottom>
	</view>
</template>

<script>
	import userChatBottom from '../../components/user-chat/user-chat-bottom.vue'
	import time from '../../common/time.js'
	import userChatList from '../../components/user-chat/user-chat-list.vue'
	export default {
		data() {
			return {
				scrollTop:0,
				style:{
					contentH:0,
					itemH:0
				},
				list:[
				]
			}
		},
		onLoad(){
			// let test = 1554970014000
			// const aa = time.gettime.gettime(test)
			// console.log(aa)
			this.getdata()
			this.initdata()
		},
		onReady(){
			this.pageToBottom()
		},
		methods: {
			// 获取初始化信息
			initdata(){
				try {
				    const res = uni.getSystemInfoSync();
					// 因为style中只允许使用px，所以这边要转换
					// 获取设备高度减去输入框高度，即默认显示内容高度
				this.style.contentH = res.windowHeight - uni.upx2px(120)
				} catch (e) {
				    // error
				}
				},
			// 获取聊天数据
			getdata(){
				let arr = [
					{
						isme:false,
						userpic:'../../static/图片素材/userpic/14.jpg',
						type:'text',
						data:'哈哈哈输入sad富商大贾撒地方感悟问题问题色给他砂糖调味啊萨特特山东省地方而去丧失对',
						time:"1554970014"
					},
					{
						isme:true,
						userpic:'../../static/图片素材/userpic/8.jpg',
						type:'img',
						data:'../../static/图片素材/2.jpg',
						time:"1555146414"
					}
				]
				for(let i =0 ; i<arr.length;i++){
				// arr[i].gstime=time.gettime.gettime(arr[i].time)
				// 下面是计算两个聊天数据时间相近时不
				arr[i].gstime=time.gettime.getChatTime(arr[i].time,i>0?arr[i-1].time:0)
				}
				this.list = arr
			},
			submit(value){
				// 构建要发送的数据
				let now = new Date().getTime()
				let obj = {
					isme:true,
					userpic:'../../static/图片素材/userpic/8.jpg',
					type:'text',
					data:value,
					time:now,
					// 获取现在发送信息时间戳和上一次发送消息的时间戳
					gstime:time.gettime.getChatTime(now,this.list[this.list.length-1].time)
				}
				this.list.push(obj)
				// 初始化执行一次不够,要每发送一次信息就执行一下计算高度,从而让scrollTop滚动条位置更新
				this.pageToBottom()
			},
			// 获取聊天页所有的元素高度，方便让滚动条自动滚动发哦我们发送的消息那
			pageToBottom(){
			let q = uni.createSelectorQuery()
				q.select('#scrollview').boundingClientRect()
				q.selectAll('.user-chat-item').boundingClientRect()
				// q.exec(res=>{
				// 	console.log(JSON.stringify(res))
				// 	res[1].map(item=>item.height).reduce((preValue,nextValue)=>{
				// 		preValue+nextValue
				// 	})
				// },this.style.itemH)
				q.exec(res=>{
					// 这里数据不对？怀疑传数据过去时数据还没渲染就被返回
					console.log(JSON.stringify(res))
					console.log(JSON.stringify(res[1]))//null
					res[1].forEach(result=>{
						this.style.itemH += result.height
					console.log(this.style.itemH,5555555555)
					})
					if(this.style.itemH > this.style.contentH){
						this.scrollTop = this.style.itemH
					}
				})
			}
		},
		components:{
			userChatBottom,
			userChatList
		}
	}
</script>

<style>
	
	/* 好一个聊天框样式 */
/* 	
.user-chat-time{
	display:flex;
	justify-content:center;
	padding:50upx 0;
	color:#A2A2A2;
	font-size:24upx;
}
.user-chat-list{
	display:flex;
	
}
.user-chat-list>image{
	width:100upx;
	height:100upx;
	border-radius:100%;
	flex-shrink:0;
}

.user-chat-list-body{
	position: relative;
	background:#F4F4F4;
	padding:25upx;
	margin-left:20upx;
	border-radius:20upx;
	margin-right:100upx;
}
.user-chat-list-body>image{
	max-width: 150upx;
	max-height: 200upx;
} */
/* 我上学时学的三角形,现在才会，明白过来 */
/* .user-chat-list-body:after{
	position:absolute;
	left:-30upx;
	right:0;
	top:30upx;
	content:'';
	width:0;
	height:0;
	border:16upx solid red;
	border-color:transparent red transparent transparent;
}

.user-chat-me{
	justify-content:flex-end;
}
.user-chat-me .user-chat-list-body{
	margin-right:20upx;
	margin-left:100upx;
}
.user-chat-me .user-chat-list-body:after{
	left:auto;
	right:-30upx;
	border-color:transparent transparent transparent red;
} */
</style>
