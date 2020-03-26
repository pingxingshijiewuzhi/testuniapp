<template>
	<view class='index-list animated rotateIn fast'>
		<view class='index-item1'>
			<view>
				<image :src="item.userpic" mode="widthFix" lazy-load></image>
				{{item.username}}
			</view>
			<view v-show='!isguanzhu' @tap='attention'>
				<view class='icon iconfont icon-zengjia'></view>
				关注
			</view>
		</view>
		<view class='index-item2' @tap='opendetail'>{{item.title}}</view>
		<view class='index-item3' @tap='opendetail'>
			<image :src="item.titlepic" mode="widthFix" lazy-load></image>
			
			<template v-if="item.type=='video'">
				<view class='index-item-play icon iconfont icon-bofang'></view>
				<view class='index-item-playinfo'>
					{{item.playnum}}次播放  {{item.long}}
				</view>	
			</template>
		</view>
		<view class='index-item4'>
			<view>
				<view :class="{'active':(infonum.index==1)}"
				@tap="operation('ding')">
				<view class='icon iconfont icon-icon_xiaolian-mian'></view>
				{{infonum.dingnum}}
				</view>
				<view :class="{'active':(infonum.index==2)}"
				@tap="operation('cai')">
					<view class='icon iconfont icon-kulian'></view>
				{{infonum.cainum}}
				</view>
			</view>
			<view>
				<view><view class='icon iconfont icon-pinglun1'></view>
				{{item.commentnum}}
				</view>
				<view><view class='icon iconfont icon-zhuanfa'></view>
				{{item.sharenum}}
				</view>
			</view>
		</view>
	</view>	
</template>

<script>
	export default {
		// props:{
		// 	item:{
		// 		type:Object
		// 	},
		// 	index:{
		// 		type:Number
		// 	}
		// },
		props:{
			item:Object,
			index:Number
		},
		data(){
			return {
				isguanzhu:this.item.isguanzhu,
				infonum:this.item.infonum
			}
		},
		methods:{
			attention(){
				// console.log(this.item)
				this.isguanzhu = true
				uni.showToast({
					title:'关注成功',
					// icon:success,
					// image:'',
				})
			},
			operation(type){
				console.log(type)
				console.log(this.infonum.index)
				switch(type){
					 case 'ding':
					 if(this.infonum.index==1){return}
					 this.infonum.dingnum++
					 if(this.infonum.index==2){
							this.infonum.cainum--
					 }
					 this.infonum.index = 1
					 break;
					 case 'cai':
					 if(this.infonum.index==2){return}
					 this.infonum.cainum++
					 if(this.infonum.index==1){
					 	this.infonum.dingnum--
					 }
					 this.infonum.index = 2
					 break
				}
			},
			// 进入详情页
			opendetail(){
				// console.log('进入详情页')
				uni.navigateTo({
					// 把数据传过去this.item
					// 对象直接传不了，得转成字符串
					// JSON.stringify(this.item)
					url:'../../pages/detail/detail?detailData='+JSON.stringify(this.item)
				})
			}
		}
	}
</script>

<style scoped>

.index-list{
	padding:20upx;
	border-bottom: 1upx solid #EFEFEF;
}
.index-item1{
	display:flex;
	justify-content: space-between;
	align-items: center;
}
.index-item1>view:first-child{
	display: flex;
	align-items: center;
	color:#999999;
}
.index-item1>view:first-child image {
	width:90upx;
	border-radius:100%;
	margin-right:10upx;
}
.index-item1>view:last-child{
	display: flex;
	align-items: center;
	border-radius:5upx;
	background-color: #F4F4F4;
	padding: 0 10upx;
}
/* .index-item1>view:last-child */
.index-item2{
	padding-top:15upx;
	font-size: 32upx;
}
.index-item3{
	padding-top:15upx;
	position:relative;
}
.index-item3>image{
	width:100%;
	border-radius: 20upx;
}
.index-item4{
	padding: 15upx 0;
	display:flex;
	justify-content: space-between;
	align-items: center;
}
.index-item4 view{
	color:#F4F4F4;
}
.index-item4>view:first-child{
	display: flex;
	align-item: center;
}
.index-item4>view:last-child{
	display: flex;
	align-item: center;
}
.index-item4>view>view{
	display: flex;
	align-items: center;
}
.index-item4>view>view:first-child{
	margin-right: 10upx;
}
.index-item4>view>view>view{
	margin-right: 10upx;
}
.index-item-play{
	position:absolute;
	font-size: 140upx;
	color:#FFFFFF;
	left:50%;
	top:50%;
	transform: translate(-50% ,-50%);
}
.index-item-playinfo{
	position:absolute;
	background: rgba(51,51,51,0.72);
	color:#FFFFFF;
	border-radius: 40upx;
	right: 8upx;
	bottom: 20upx;
	font-size: 22upx;
	padding: 0 12upx;
}

.index-item4 active,.index-item4 .active>view{
	color:#09BB07;
}
</style>
