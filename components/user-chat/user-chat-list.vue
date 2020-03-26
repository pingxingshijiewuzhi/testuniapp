<template>
	<view class='user-chat-item'>
		<view class='user-chat-time' v-if='item.gstime'>{{item.gstime}}</view>
		<view class='user-chat-list ' :class="[item.isme ?'user-chat-me':'']">
				<image v-if='!item.isme' :src="item.userpic" mode="widthFix" lazy-load></image>
				<view class='user-chat-list-body'>
					<!-- 文字 -->
					<text v-if="item.type=='text'">
						{{item.data}}
					</text>
					<!-- 图片 -->
					<image  v-if="item.type=='img'" :src="item.data" mode="widthFix" lazy-load></image>
				</view>
				<image v-if='item.isme' :src="item.userpic" mode="widthFix" lazy-load></image>	
			
		</view>	
	</view>
</template>

<script>
	export default {
		props:{
		item:Object,
		index:Number
		}
	}
</script>

<style scoped>
	.user-chat-item{
		padding:0 20upx;
	}
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
	}
	/* 我上学时学的三角形,现在才会，明白过来 */
	.user-chat-list-body:after{
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
	}
</style>
