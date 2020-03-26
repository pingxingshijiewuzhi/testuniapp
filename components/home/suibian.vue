<template>
	<view class='other-login'>
		<!-- <template v-if='providerList.length'> -->
			<block v-for='(item,index) in  providerList' :key='index'>
				<view class='other-login-item' @tap='tologin(item)'>
					<!-- <view class="icon iconfont icon-QQ"></view> -->
					<!-- <view :class="['icon iconfont icon-'+item.icon]"></view> -->
					<view class='icon iconfont' :class="['icon-'+item.icon]"></view>
				</view>			
			</block>
		<!-- </template> -->
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
		    this.getLoginAuth()
		},
		methods:{
			// 获取服务供应商。
			getLoginAuth(){
				uni.getProvider({
				    service: 'oauth',
				    success: (result) => {
						console.log('为啥进入不了这个获取参数列表')
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
				            }
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
			// 用获取回来的providerid来登录
			tologin(provider) {
			    uni.login({
			        provider: provider.id,
			        // #ifdef MP-ALIPAY
			        scopes: 'auth_user', //支付宝小程序需设置授权类型
			        // #endif
			        success: (res) => {
						console.log(JSON.stringify(res))
			            console.log('login success:', res);
			            // 更新保存在 store 中的登录状态
						console.log("登录成功，保存到本地存储，修改当前用户状态")
			            // this.login(provider.id);
			        },
			        fail: (err) => {
			            console.log('login fail:', err);
			        }
			    });
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

