<template>
	<view class='common-list animated fadeInLeft fast'>
		<view class='common-list-l'>
			<image :src="item.userpic" mode="widthFix" lazy-load></image>
		</view>
		
		<view class='common-list-r'>
			<view class='rfirest'>
				<view class='nick'>
					{{item.username}}
					<tag-sex-age :sex='item.sex' :age='item.age'></tag-sex-age>
				</view>
				<view v-show='!isguanzhu' 
				@tap='attention'
				class='icon iconfont icon-zengjia'>关注</view>
			</view>
			<view>{{item.title}}</view>
			<view class='rthree'>
				<!-- 图片 -->
				<image v-if='item.titlepic' :src='item.titlepic' mode="widthFix" lazy-load></image>
				<!-- 视频 -->
				<template v-if='item.video'>
				<view class='index-item-play icon iconfont icon-bofang'></view>
				<view class='index-item-playinfo'>
					{{item.video.looknum}}次播放  {{item.video.long}}
				</view>		
				</template>
				<!-- 分享 -->
				<template v-if='item.share'>	
				<view class='common-list-share'>
					<image :src="item.share.titlepic" mode="widthFix"></image>
					<view>{{item.share.title}}</view>
				</view>
				</template>
			</view>
			<view class='rfour'>
				<view>{{item.path}}</view>
				<view class='flexclass'>
					<view class='icon iconfont icon-zhuanfa'>{{item.sharenum}}</view>
					<view class='icon iconfont icon-pinglun1'>{{item.commentnum}}</view>
					<view class='icon iconfont icon-dianzan1'>{{item.goodnum}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import tagSexAge from './tag-sex-age.vue'
	export default {
		props:{
			item:Object,
			index:Number
		},
		data(){
			return {
				isguanzhu:this.item.isguanzhu
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
			}
		},
		components:{
			tagSexAge
		}
	}
</script>

<style scoped>
	@import '../../common/list.css'
</style>
