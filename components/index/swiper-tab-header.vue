<template>
	<view class='uni-tab-bar'>
		<scroll-view scroll-x class="uni-swiper-tab" :style='scrollStyle'>
			<block v-for='(item,index) in  tabBars' :key='index'>
			<view class='swiper-tab-list'
			 :class="{'active':(tabIndex==index)}"
			 @tap='tabClick(index)'
			 :style='scrollItemStyle'>
				{{item.name}}{{item.num?item.num:''}}
				<view class='swiper-tab-line'></view>
			</view>
			</block>
		</scroll-view>
	</view>
</template>

<script>
	export default{
		props:{
			// tabBars:{
			// 	type:Array
			// },
			// tabIndex:{
			// 	type:Number
			// }
			tabBars:Array,
			tabIndex:Number,
			scrollStyle:{
				type:String,
				default:''
			},
			scrollItemStyle:{
				type:String,
				default:''
			}
		},
		methods:{
			tabClick(index){
				// this.tabIndex = index
				this.$emit('tabIndexChange',index)
			}
		}
	}
</script>

<style scoped>
	/* 原来引入的uni.css里定义了active
		怪不得引入这三个类名
		uni-tab-bar
		uni-swiper-tab
		swiper-tab-list*/
	/* 	.uni-tab-bar{
			height:100vh;
		} */
		/* uni.css里有uni-swiper-tab,我这里覆盖,把height:100rpx修改为100upx */
		.uni-swiper-tab{
				width: 100%;
				white-space: nowrap;
				line-height: 100rpx;
				height: 100upx;
				border-bottom: 1px solid #c8c7cc;
		}
	.uni-tab-bar .active{
		color:#343434;
	}
	.swiper-tab-list{
		color:#969696;
		font-weight: bold;
		}
	.active	.swiper-tab-line{
		border-bottom: 6upx solid #FEDE33;
		width:70upx;
		margin:0 auto;
		border-top: 6upx solid #FEDE33;
		border-radius: 20upx;
	}
	
</style>
