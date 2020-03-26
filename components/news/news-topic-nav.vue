<template>
	<view class='topic-nav'>
		<view>
			<view>热门分类</view>
			<view @tap='opentopicnav'>
				更多 <view class='icon iconfont icon-jinru'></view>
			</view>
		</view>
		<view>
		<block v-for='(item,index) in nav' :key='index'>
			<view>{{item.name}}</view>
		</block>
		</view>
	</view>
</template>

<script>
	export default{
		props:{
			nav:Array
		},
		methods:{
			opentopicnav(){
				uni.navigateTo({
					url:'../../pages/topic-nav/topic-nav'
				})
		}
		}
	}
</script>

<style scoped>
	.topic-nav{
		border-top:1upx solid #EEEEEE;
		border-bottom:1upx solid #EEEEEE;
		padding:20upx;
		}
	.topic-nav>view:first-child{
		display:flex;
		align-items: center;
		justify-content:space-between;
		margin-bottom: 10upx;
		font-size: 28upx;
	}
	.topic-nav>view:first-child>view:last-child{
		display:flex;
		align-items: center;
	}
	.topic-nav>view:last-child{
		display:flex;
		align-items: center;
	}
	.topic-nav>view:last-child>view{
		flex: 1;
		color:#9E9E9E;
		background-color: #EEEEEE;
		border-radius: 10upx;
		margin:0 10upx;
		text-align: center;
	}
</style>
