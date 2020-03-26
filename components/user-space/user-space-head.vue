<template>
	<view class='user-space-head'>
		<image :src="getBgImg" mode='widthFix' lazy-load
		@tap.stop='chagneBgImg'></image>
		<view class='user-space-head-info'>
			<image :src='userinfo.userpic' mode='widthFix' lazy-load></image>
			<view class='user-space-margin nickname'>
				 {{userinfo.username}}
				 <tag-sex-age :sex='userinfo.sex' :age='userinfo.age'></tag-sex-age>
			</view>
			<view class='icon iconfont  user-space-margin user-space-head-btn'
			:class="[isattention?'active':'icon-zengjia']" @tap.stop='attention'>
				{{isattention?"已关注":"关注"}}
			</view>
		</view>
	</view>
</template>

<script>
		import tagSexAge from '../common/tag-sex-age.vue'
	export default{
		components:{
			tagSexAge
		},
		props:{
			userinfo:Object
		},
		data(){
			return {
				isattention:this.userinfo.attention,
				bgimg:this.userinfo.bgimg
			}
		},
		computed:{
			getBgImg(){
				return '../../static/图片素材/datapic/'+this.bgimg+'.jpg'
			}
		},
		methods:{
			// 关注按钮的切换
			attention(){
				this.isattention = !this.isattention
			},
			// 切换背景图
			chagneBgImg(){
				let num = parseInt(this.bgimg) 
				this.bgimg = num < 4 ? ++num : 1
			}
		}
	}
</script>

<style scoped>
	.user-space-head{
		display:flex;
		justify-content:center;
		align-items:center;
		position:relative;
		height:500upx;
		overflow:hidden;
	}
	.user-space-head>image{
		width:100%;
	}
	.user-space-head-info{
		display:flex;
		justify-content:center;
		align-items:center;
		flex-direction:column;
		position:absolute;
		top:150upx;
	}
	.user-space-head-info>image{
		width:100upx;
		height:100upx;
		border-radius:100%;
	}
	.user-space-head-info>view:first-of-type{
		color:#ffffff;
		font-size:35upx;
		font-weight:bold;
		text-shadow:2upx 2upx 10upx #333333;
	}
	.nickname{
		display:flex;
		justify-content: center;
		align-items:center;
	}
	
	.user-space-head-btn{
		background-color: #FFE933;
		color:#333333;
		border:1upx solid #FFE933;
		padding:0 15upx;
		font-size: 28upx;
		border-radius:10upx;
	}
	.active{
		background:none;
		color:#FFFFFF;
		border:1upx solid #FFFFFF
	}
</style>
