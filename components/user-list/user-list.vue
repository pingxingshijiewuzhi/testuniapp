<template>
	<view class='user-list animated fadeInLeft fast' @tap='openChat'>
		<image :src='item.userpic' mode="widthFix" lazy-load></image>
		<view>
			<view>{{item.username}}</view>
			<view style='display:inline-block'>
			<tag-sex-age :age='item.age' :sex='item.sex'></tag-sex-age>
			</view>
		</view>
		<!-- <view class='icon iconfont icon-xuanze-yixuan'></view> -->
		
		<view class='icon iconfont icon-zengjia1'
		:class="[item.isguanzhu?'hello':'']"></view>
	</view>
</template>

<script>
		import tagSexAge from '../../components/common/tag-sex-age.vue'
	export default {
		props:{
			item:Object
		},
		components:{
			tagSexAge
		},
		methods:{
			openChat(){
				console.log('555')
				uni.navigateTo({
					url:'../../pages/user-chat/user-chat'
				})
			}
		}
	}
</script>

<style scoped>
	.user-list{
		display:flex;
		align-items:center;
		padding:20upx 0;
		border-bottom:1upx solid #EEEEEEE;
	}
	.user-list>image{
		width:100upx;
		border-radius:100%;
		height:100upx;
		flex-shrink:0;
		margin-right:20upx;
	}
	.user-list>view:first-of-type{
		flex:1;
	}
	.user-list>view:first-of-type>view:first-child{
		font-size:35upx;
	}
	.user-list>view:last-of-type{
		width:80upx;
		color:#CCCCCC;
	}
	.hello{
		color: #F8791B !important;
		}
</style>
