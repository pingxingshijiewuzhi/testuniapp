<template>
	<view class='animated fadeInLeft fast'  v-if='show'>
		<view class='more-share-model'  @tap='showShare'></view>
		<view class='more-share' >
			<view class='more-share-title'>分享到</view>
			<scroll-view scroll-x class='more-share-body'>
				<block v-for='(val,index) in providerList' :key='index'>
					<view class='more-share-body-item' hover-class='more-share-body-hover'
					@tap='share(val)'>
						<view class='icon iconfont'
						:class="['icon-'+val.zicon, 'more-share-'+val.zclass]"></view>
						<view>{{val.name}}</view>
					</view>	
				</block>
				
				<view class='more-share-body-item' hover-class='more-share-body-hover'>
					<view class='icon iconfont icon-QQ more-share-qq'></view>
					<view>其他</view>
				</view>
			</scroll-view>
			<view class='more-share-bottom' hover-class='more-share-body-hover'
			@tap='showShare'>取消</view>
		</view>
	</view>
</template>

<script>
	export default{
		props:{
			show:Boolean
		},
		data() {
			return {
				title: 'share',
				shareText: 'uni-app可以同时发布成原生App、小程序、H5，邀请你一起体验！',
				href:"https://uniapp.dcloud.io",
				image: '',
				shareType:1,
				providerList: []
			}
		},
		methods:{
			// 显示分享
			showShare(){
				this.$emit('showShare')
			},
			compress(){//压缩图片 图文分享要求分享图片大小不能超过20Kb
				console.log('开始压缩');
				let img = this.image;
				return new Promise((res) => {
					var localPath = plus.io.convertAbsoluteFileSystem(img.replace('file://', ''));
					console.log('after' + localPath);
					// 压缩size
					plus.io.resolveLocalFileSystemURL(localPath, (entry) => {
						entry.file((file) => {// 可通过entry对象操作图片 
							console.log('getFile:' + JSON.stringify(file));
							if(file.size > 20480) {// 压缩后size 大于20Kb
								plus.zip.compressImage({
									src: img,
									dst: img.replace('.jpg', '2222.jpg').replace('.JPG', '2222.JPG'),
									width: '10%',
									height: '10%',
									quality: 1,
									overwrite: true
								}, (event) => {
									console.log('success zip****' + event.size);
									let newImg = img.replace('.jpg', '2222.jpg').replace('.JPG', '2222.JPG');
									res(newImg);
								}, function(error) {
									uni.showModal({
										content:'分享图片太大,需要请重新选择图片!',
										showCancel:false
									})
								});
							}
						});
					}, (e) => {
						console.log('Resolve file URL failed: ' + e.message);
						uni.showModal({
							content:'分享图片太大,需要请重新选择图片!',
							showCancel:false
						})
					});
				})
			}
		},
		onLoad(){
			uni.getProvider({
				service: 'share',
				success: (e) => {
					let data = []
					for (let i = 0; i < e.provider.length; i++) {
						switch (e.provider[i]) {
							case 'weixin':
								data.push({
									name: '微信好友',
									id: 'weixin',
									zicon:'weixin',
									zclass:'wx',
									sort:0
								})
								data.push({
									name: '微信朋友圈',
									id: 'weixin',
									type:'WXSenceTimeline',
									zicon:'',
									zclass:'pyq',
									sort:1
								})
								break;
							case 'sinaweibo':
								data.push({
									name: '新浪微博',
									id: 'sinaweibo',
									zicon:'xinlangweibo',
									zclass:'wb',
									sort:2
								})
								break;
							case 'qq':
								data.push({
									name: 'QQ好友',
									id: 'qq',
									zicon:'QQ',
									zclass:'qq',
									sort:3
								})
								break;
							default:
								break;
						}
					}
					this.providerList = data.sort((x,y) => {
						return x.sort - y.sort
					});
				},
				fail: (e) => {
					console.log('获取分享通道失败', e);
					uni.showModal({
						content:'获取分享通道失败',
						showCancel:false
					})
				}
			});
		}
	}
</script>

<style scoped>
	/* 分享样式 */
		/* 分享的模板 */
		.more-share-model{
			/* background-color: #333333; */
			/* 换成透明色 */
			background:rgba(51,51,51,0.49);
			position: fixed;
			bottom:0;
			left:0;
			right:0;
			top:0;
			z-index:98
		}
	
	.more-share{
		position: fixed;
		bottom:0;
		left:0;
		right:0;
		background: #FFFFFF;
		z-index:99;
		}
		.more-share-title, .more-share-bottom{
			display: flex;
			justify-content: center;
			font-size:32upx;
			padding:24upx;
		}
		.more-share-body{
			display:flex;
			align-items:center;
			white-space: nowrap;
			hieght:200upx;
			width:100%;
			border-bottom:1upx solid #EEEEEE;
			line-height:200upx!important;
		}
		.more-share-body-item{
			width:25%;
			display:inline-flex;
			align-items:center;
			justify-content: center;
			flex-direction:column;
			height:100%;
		}
		.more-share-body-item>view:first-child{
			width:100upx;
			height:100upx;
			border-radius:100%;
			font-size: 55upx;
			color: #FFFFFF;
			text-align: center;
		}
		.more-share-body-hover{
			background: #EEEEEE;
		}
		.more-share-body-item>view:last-child{
			color:#7A7A7A;
		}
		.more-share-wx{
			background: #2AD19B;
		}
		.more-share-pyq{
			background: #514D4C;
		}
		.more-share-wb{
			background: #EE5E5E;
		}
		.more-share-qq{
			background: #4A73BA;
		}
</style>
