<template>
	<view class='other-login'>
		<view class='other-login-item'>
			<view class='icon iconfont icon-QQ'></view>
		</view>
		<view class='other-login-item'>
			<view class='icon iconfont icon-weixin'></view>
		</view>
		<view class='other-login-item' @tap='tryevent'>
			<view class='icon iconfont icon-xinlangweibo'></view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				 providerList: []
			}
		},
		onLoad() {
			// 获取服务供应商。
		    uni.getProvider({
		        service: 'oauth',
		        success: (result) => {
					console.log('5555')//为啥进入不了？不执行这个成功函数
		            this.providerList = result.provider.map((value) => {
		                let providerName = '';
						let icon = ''
		                switch (value) {
		                    case 'weixin':
		                        providerName = '微信登录'
								icon='weixin'
		                        break;
		                    case 'qq':
		                        providerName = 'QQ登录'
								icon='QQ'
		                        break;
		                    case 'sinaweibo':
		                        providerName = '新浪微博登录'
								icon='xinlangweibo'
		                        break;

		                    case 'alipay':
		                        providerName = '支付宝登录'
								icon=''
		                        break;
		                    case 'apple':
		                        providerName = '苹果登录'
								icon=''
		                        break;
		                }
						console.log(icon)
		                return {
		                    name: providerName,
							icon:icon,
		                    id: value
		                }
		            });
		
		        },
		        fail: (error) => {
		            console.log('获取登录通道失败', error);
		        }
		    });
		},
		methods:{
			tryevent(){
				console.log(this.providerList)
			}
		}
	}
</script>

<style scoped>
.other-login{
	display:flex;
}
.other-login-item{
	flex:1;
	display:flex;
	justify-content:center;
	align-items:center;
	
}
.other-login-item>view{
	width:100upx;
	height:100upx;
	color:#FFFFFF;
	border-radius:100%;
	font-size:55upx;
	text-align: center;
}
.other-login-item .icon-QQ{
	background-color: #2CAEFC;
}
.other-login-item .icon-weixin{
	background-color: #2BD19B;
}
.other-login-item .icon-xinlangweibo{
	background-color: #FC7729;
}
</style>
