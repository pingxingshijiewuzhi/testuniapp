<template>
	<view>
		<uni-nav-bar :fixed='true' :statusBar="true" :border='false' @click-right='openAdd'>
			    <view slot="left" >
					<view class='nav-left'>
					<view class='icon iconfont icon-qiandao'></view>
					</view>
				</view>
			<view class='nav-center'>
				<view v-for='(item,index) in  tabBars' :key='item.id'>
					<view class='flexcenter' :class="{'active':(index==tabIndex)}" @tap='changeTab(index)'>
					{{item.name}}
					<view v-if='(index==tabIndex)' class='nav-center-line'></view>
					</view>
				</view>
			</view>
			    <view slot="right">
					<view class='nav-right'>
					<view class='icon iconfont icon-bianji'></view>
					</view>
				</view>
		</uni-nav-bar>
	</view>
</template>

<script>
		import uniNavBar from "../../components/uni-nav-bar/uni-nav-bar.vue"
	export default {
		components:{
			uniNavBar
		},
		props:{
			tabBars:Array,
			tabIndex:Number
		},
		methods:{
			changeTab(index){
				this.$emit('change-tabbar',index)
			},
			openAdd(){
			uni.navigateTo({
				url:'../add-input/add-input'
			})		
			}
		}
	}
</script>

<style scoped>
	.nav-left>view,.nav-right>view{
			font-size:40upx;
		}
		.nav-left>view{
			color:#FF9619;
		}
	.nav-left{
		margin-right:16upx;
	}
	.nav-right{
		width:100%;
		display:flex;
		justify-content:center;
		align-items:center;
	}
	.nav-center{
		width:100%;
		margin-left: -20upx;
		display: flex;
		justify-content: center;
		align-items: center;
		position:relative;
	}
	.nav-center view{
		font-size: 32upx;
		font-weight: bold;
		padding:0  15upx;
		color:#969696;
	}
	.flexcenter{
		display:flex;
		justify-content: center;
	}
	.nav-center .nav-center-line{
		border-top: 5upx solid #FEDE33;
		border-top:5upx solid #FEDE33;
		border-radius: 20upx;
		width:40upx;
		position:absolute;
		bottom: 12upx;
	}
	.active{
		color:#333333 !important;
	}
	
</style>
