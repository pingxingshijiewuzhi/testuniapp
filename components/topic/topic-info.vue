<template>
	<view>
		<!-- 模糊背景 -->
		<view class='topic-bg'>
			<image :src="item.titlepic" mode="aspectFill" lazy-load></image>
		</view>
		<!-- 话题信息 -->
		<veiw class='topic-info'>
			<view class='topic-info-o'>
				<image :src="item.titlepic"  lazy-load></image>
				<view>#{{item.title}}#</view>
			</view>
			<view class='topic-info-t'>
				<view>动态 {{item.totalnum}}</view>
				<view>几日 {{item.todaynum}}</view>
			</view>
			<view class='topic-info-th'>
				{{item.desc}}
			</view>
		</veiw>
	</view>
</template>

<script>
	export default {
		props:{
			item:Object
		}
	}
</script>

<style scoped>
	.topic-bg{
		width:100%;
		height:300upx;
		position: relative;
		overflow: hidden;
	}
	.topic-bg image{
		width:100%;
		position:absolute;
		filter: blur(10px);
	}
	
	.topic-info{
		padding:0 25upx;
	}
	.topic-info-o{
		display: flex;
		align-items:center;
		position:relative;
	}
	.topic-info-o>image{
		width:150upx;
		height:150upx;
		border-radius:20upx;
		position:absolute;
		top:-75upx;
	}
	.topic-info-o>view{
		font-size:35upx;
		margin-left: 150upx;
		flex:1;
	}
	.topic-info-t{
		display:flex;
		align-items:center;
		padding:20upx 0;
	}
	.topic-info-t view{
		color:#cdcdcd;
	}
	.topic-info-th{
		color:#A3A3A3;
		font-size:32upx;
		padding-bottom: 10upx;
	}
</style>
