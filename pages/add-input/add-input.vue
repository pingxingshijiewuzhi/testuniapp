<template>
	<view>
		<uni-nav-bar :statusBar="true" rightText="发布"
		leftIcon="back" @click-left='back' @click-right='submitClick'>
		<view class='flexbox' @tap='changestatus'>
			{{yinsi}}
			<view class='icon iconfont icon-xialazhankai'></view>
		</view>
			
		</uni-nav-bar>
		<!-- 多行输入框 -->
		<view class='uni-textarea'>
		<textarea name="" id="" placeholder="说一句话吧" v-model='text'></textarea>
		</view>
		<!-- 上传多图 -->
		<uploud-images @upload="upload" @del='delImageList' :image-list="imglist"></uploud-images>
	</view>
</template>

<script>
	let changeList = ['所有人可见', '仅自己可见']
	import uniNavBar from '../../components/uni-nav-bar/uni-nav-bar.vue'
	import uploudImages from "../../components/common/uploud-images.vue"
	export default {
		data() {
			return {
				yinsi:'所有人可见',
				text:'',
				imglist:[]
			}
		},
		methods: {
			back(){
				uni.navigateBack({
					delta:1
				})
			},
			submitClick(){
				
			},
			changestatus(){
				uni.showActionSheet({
				    itemList: changeList,
				    success(res){
							this.yinsi = changeList[res.tapIndex]
				    }
				});
			},
			upload(img){
				console.log(img)
			},
			delImageList(index){
				this.imageList.split(index,1)
			}
		},
		components:{
			uniNavBar,
			uploudImages
		}
	}
</script>

<style>
.flexbox{
	display:flex;
	justify-content:center;
	align-items: center;
}
.uni-textarea{
	border:1upx solid #EEEEEE
}
</style>
