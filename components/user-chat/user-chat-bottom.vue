<template>
	<view class='user-chat-bottom'>
		<input type="text" placeholder='文明发言' v-model='text'>
		<view class='icon iconfont icon-fabu' @tap='submit'></view>
	</view>
</template>

<script>
	export default{
		data(){
			return {
				text:''
			}
		},
		methods:{
			submit(){
				this.$emit('submit',this.text)
				this.text=''
			}
		}
	}
</script>

<style scoped>
	.user-chat-bottom{
		display:flex;
	/* 	justify-content:space-between; */
		align-items:center;
		position:fixed;
		left:0;
		right:0;
		bottom:0;
		height:120upx;
		/* background:#fffffff; */
		background-color:white;
		border-top:1upx solid #EEEEEE;
		padding:0 20upx;
	}
	.user-chat-bottom>input{
		flex:1;
		margin-right:20upx;
		padding:10upx 20upx;
		border-radius:10upx;
		background-color: #F7F7F7;
	}
	.user-chat-bottom>view{
		width:80upx;
		text-align: center;
		font-size: 45upx;
		color: #000000;
	}
</style>
