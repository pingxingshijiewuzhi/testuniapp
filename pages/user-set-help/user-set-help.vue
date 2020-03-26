<template>
	<view>
			<uni-collapse>
				<block v-for="(item,index) in list" :key="index">
					<uni-collapse-item :title="item.title" :show-animation="true" 
					:contentdata="item.content"></uni-collapse-item>
				</block>
			</uni-collapse>
		<view class='bodybox'>
			
		<button class='user-set-btn'
		type='primary' @tap="openFeedback">意见反馈</button>
		</view>
	</view>
</template>

<script>
	import uniCollapse from '../../components/uni-collapse/uni-collapse.vue'
	import uniCollapseItem from '../../components/uni-collapse-item/uni-collapse-item.vue'
	export default {
		components:{
			uniCollapse,
			uniCollapseItem
		},
		data() {
			return {
				list:[
					{
						title:"客服什么时候上线？",
						content:"123"
					},
					{
						title:"忘记账号/昵称/密码怎么办？",
						content:"111111111"
					},
					{
						title:"怎么搜索/查找/关注/取关用户？",
						content:"222222"
					}
				]
			}
		},
		methods: {
				openFeedback(){
							uni.navigateTo({
								url: '/pages/user-feedback/user-feedback',
							});
						}
		}
	}
</script>

<style>
.bodybox{
		padding:0 20upx;
}
.user-set-btn{
	width:100%;
	padding:20upx 0;
	color:#333333!important;
	background-color: #FFE933!important;
	border:0!important;
}

</style>
