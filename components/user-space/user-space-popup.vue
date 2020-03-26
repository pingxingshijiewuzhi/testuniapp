<template>
	<view>
		<view class='papar-left-popup-mask' v-if='status' @tap='hidepopup'></view>
		<view class='papar-left-popup' v-if='status'>
			<view hover-class="paper-left-popup-h" @tap='lahei'> 
			<view class='icon iconfont icon-sousuo'></view> 
			拉黑
			</view>
			<view hover-class="paper-left-popup-h" @tap='remark'>
				<view class='icon iconfont icon-qingchu'></view>
				 备注
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		props:{
			status:Boolean
		},
		methods:{
			hidepopup(){
				this.$emit('hidepopup')
			},
			lahei(){
				this.$emit('lahei')
			},
			remark(){
				this.$emit('remark')
			}
		}
	}
</script>

<style scoped>
	.papar-left-popup{
		position:fixed;
		right:0;
		top:100upx;
		background:#FFFFFF;
		z-index: 99;
		width: 55%;
		box-shadow: 1upx 1upx 20upx 20upx #CCCCCC;
		}
	.papar-left-popup>view{
		display:flex;
		align-items:center;
		padding:20upx;
		font-size:25upx;
	}
	.papar-left-popup>view>view:first-child{
		margin-right:10upx;
		font-weight: bold;
	}
	
	.paper-left-popup-h{
		background-color: #EEEEEE;
	}
	.papar-left-popup-mask{
		position:fixed;
		left:0;
		right:0;
		top:0;
		bottom:0;
	}
</style>

