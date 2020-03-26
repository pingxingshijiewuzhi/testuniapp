<template>
	
	<view class='paper-list animated fadeInLeft fast' >
		<image :src="item.userpic" 
		mode="widthFix" lazy-load></image>
		<view>
			<view>{{item.username}}<view>{{item.time}}</view> </view>
			<view>{{item.data}}
			<template v-if='item.noreadnum>0'>
			<uni-badge :text="item.noreadnum" type="error" @click="bindClick"></uni-badge>
			</template>
			</view>
		</view>
	</view>
	
</template>

<script>
	import uniBadge from '../../components/uni-badge.vue'
	export default{
		props:{
			item:Object,
			index:Number
		},
			
		components:{
			uniBadge
		},
		methods:{
		}
	}
</script>

<style scoped>
	.paper-list{
		border-bottom:1upx solid #EEEEEE;
		padding:20upx 0;
		display:flex;
		align-items:center;
	}
	.paper-list>image{
		width:100upx;
		height:100upx;
		border-radius:10upx;
		margin-right:20upx;
		flex-shrink:0;
	}
	.paper-list>view{
		flex:1
	}
	.paper-list>view>view{
		display:flex;
		align-items:center;
		justify-content: space-between;
	}
	.paper-list>view>view:first-child{
		font-size: 32upx;
	}
	.paper-list>view>view:first-child>view{
		color:#CBCBCB;
	}
	.paper-list>view>view:last-child{
		color:#999999;
	}
</style>
