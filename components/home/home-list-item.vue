<template>
	<view class='flexlist' hover-class="home-list-hover"
	@tap='clickevent(item)'>
		<view class='flexlist-item'>
			<view v-if='item.icon'
			:class="['icon iconfont icon-'+item.icon]"></view>
			{{item.name}}
		</view>
		<view class='icon iconfont icon-jinru'></view>	
	</view>
</template>

<script>
	export default{
		props:{
			item:Object,
			index:Number
		},
		methods:{
			clickevent(item){
				switch(item.clicktype){
					case "navigateTo":
					if(item.url){
					uni.navigateTo({url:item.url})
					}
					break
					case "clear":
					uni.showModal({
						title:'提示',
						content:'是否清除缓存',
						confirmText:"立即清除",
						success:res=>{
							if(res.confirm){
								uni.clearStorage();
								uni.showToast({
									title:'清除缓存成功'
								})
							}
						}
					})
					break
				}
			}
		}
	}
</script>

<style scoped>
	.home-list-hover{
		color:#F4F4F4;
	}
	.flexlist{
		display:flex;
		justify-content: space-between;
		align-items:center;
		padding:20upx;
		border-top:1upx solid #EEEEEE;
		border-bottom:1upx solid #EEEEEE;
	}
	.flexlist>view:last-child{
		color:#CCCCCC;
	}
	.flexlist-item{
		display:flex;
	}

</style>
