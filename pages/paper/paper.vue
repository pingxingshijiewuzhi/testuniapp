<template>
	<view class='currentbody'>
		<!-- 操作菜单 -->
		<paper-left-popup :status='status' @openfrind='openfrind'
		@clean='clean' @hidepopup='hidepopup'></paper-left-popup>
		<!-- 小纸条列表 -->
		<block v-for='(item,index) in list' :key='index'>
		<paper-list :item='item' :index='index'></paper-list>
		</block>
		<!-- 上拉加载 -->
		<load-more :loadtext='loadtext'></load-more>
	</view>
</template>

<script>
	import paperList from '../../components/paper/paper-list.vue'
	import loadMore from '../../components/common/load-more.vue'
	import paperLeftPopup from '../../components/paper/paper-left-popup.vue'
	export default {
		data() {
			return {
				status:false,
				loadtext:'上拉加载更多',
				list:[
					{
						userpic:'../../static/图片素材/datapic/20.jpg',
						username:'昵称',
						time:'10:54',
						data:'我是信息',
						noreadnum:2
					},
					{
						userpic:'../../static/图片素材/datapic/20.jpg',
						username:'昵称',
						time:'10:54',
						data:'我是信息',
						noreadnum:0
					},
					{
						userpic:'../../static/图片素材/datapic/20.jpg',
						username:'昵称',
						time:'10:54',
						data:'我是信息',
						noreadnum:0
					},
					{
						userpic:'../../static/图片素材/datapic/20.jpg',
						username:'昵称',
						time:'10:54',
						data:'我是信息',
						noreadnum:2
					}
				]
				
			}
		},
		// 监听原声导航点击
		onNavigationBarButtonTap(e){
			//来判断点击返回的index来确定导航栏那个按钮
			// console.log(JSON.stringify(e.index))
			switch(e.index){
				case 0:
				uni.navigateTo({
					url:"../user-list/user-list"
				})
				this.showpopup()
				break;
				case 1:
				this.showpopup()
				break
			}
		},
		methods: {
			// 获取数据
			getDate(){
				 setTimeout(()=>{
				let arr = [
					{
						userpic:'../../static/图片素材/datapic/20.jpg',
						username:'昵称111',
						time:'10:54',
						data:'我是信息',
						noreadnum:2
					},
					{
						userpic:'../../static/图片素材/datapic/20.jpg',
						username:'昵称222',
						time:'10:54',
						data:'我是信息',
						noreadnum:0
					},
					{
						userpic:'../../static/图片素材/datapic/20.jpg',
						username:'昵称333',
						time:'10:54',
						data:'我是信息',
						noreadnum:0
					},
					{
						userpic:'../../static/图片素材/datapic/20.jpg',
						username:'昵称444',
						time:'10:54',
						data:'我是信息',
						noreadnum:2
					},
				]
				this.list = arr
				uni.stopPullDownRefresh();
				        }, 1000);
			},
			loadmore(){
				if(this.loadtext != '上拉加载更多'){return}
				this.loadtext = '加载中'
				setTimeout(()=>{
					let obj={
						userpic:'../../static/图片素材/datapic/20.jpg',
						username:'昵称444',
						time:'10:54',
						data:'我是信息',
						noreadnum:2
					}
					this.list.push(obj)
					this.loadtext = '上拉加载更多'
				},1000)
				// this.newList[index].loadtext = '没有更多数据了'
			},
			openfrind(){
				this.hidepopup()
			},
			clean(){
				this.hidepopup()
			},
			hidepopup(){
				this.status=false;
			},
			showpopup(){
				this.status=true
			}
		},
		onPullDownRefresh(){
			this.getDate()
		},
		onReachBottom(){
			this.loadmore()
		},
		components:{
			paperList,
			loadMore,
			paperLeftPopup
		}
	}
</script>

<style>
.currentbody{
	padding:0 30upx;
}


</style>
