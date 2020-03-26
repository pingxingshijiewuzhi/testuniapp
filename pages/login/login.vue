<template>
	<view>
		<!-- 状态栏 -->
		<uni-status-bar bgcolor='#FFE933'></uni-status-bar>
		<!-- 关闭按钮 -->
		<view class='icon iconfont icon-guanbi' @tap='back'></view>
		<!-- 引入背景图 -->
		<image class='loginhead' src='../../static/common/loginhead.png'
		 mode='widthFix' lazy-load></image>
		 
		 <view class='bodybox'>
			 <!-- 账号密码登录 -->
			<template v-if='!status'>
				<input type="password" v-model='username'
				class='uni-input common-input'
				 placeholder="昵称/手机号/邮箱">
				 
				 <view class='login-input-box'>
					<input type="password" v-model='password'
					class='uni-input common-input forget-input' 
					placeholder="请输入密码"> 
					<view class='forget'>忘记密码</view>
				 </view>
			</template>
				<!-- 手机验证码登录 -->
			<template v-else>
				<view class='login-input-box'>
					 <view class='phone'>+86</view>
					 <input type="text" v-model='phone'
						class='uni-input common-input phone-input'
						 placeholder="手机号">
				</view>
				<view class='login-input-box'>
					<input type="password"  v-model='verification'
					class='uni-input common-input forget-input' 
					placeholder="请输入验证码"> 
					<view class='forget  verification' @tap='getVerification'>
						<view>{{!codetime?'获取验证码':codetime+'s'}}</view>
					</view>
				</view>
			</template>

			
		 	
		 	<button class='user-set-btn'
		 	:class="{'user-set-btn-disable':disabled}"
		 	:disabled='disabled'
		 	:loading='loading'
		 	type='primary' @tap='submit'>登录</button>
		 </view>
		 
		 <!-- 登录状态切换 -->
		 <view class='login-status login-padding .login-font-color' 
		 @tap='changeStatus'>
			 {{status ? '账号密码登录':'验证码登录'}} 
			 <view class='icon iconfont icon-jinru .login-font-color'></view>
		 </view>
		 
		 <!-- 第三方登录 -->
		 <view class='other-login-title login-padding .login-font-color'>第三方登录</view>
		 <other-login></other-login>
		 
		 <!-- 协议 -->
		 <view class='protocol login-padding .login-font-color'>
			 注册即代表您同意《仿糗事百科用户协议》
		 </view>
	</view>
</template>

<script>
	import uniStatusBar from '../../components/uni-status-bar/uni-status-bar.vue'
	import otherLogin from '../../components/home/other-login.vue'
	export default {
		data() {
			return {
				status:false,//false代表账号密码登录，true是手机验证码登录
				disabled:true,
				loading:false,
				username:'',
				password:'',
				phone:'',
				verification:"",
				codetime:0
			}
		},
		watch:{
			username(){
				this.onBtnChange()
			},
			password(){
				this.onBtnChange()
			},
			phone(){
				this.onBtnChange()
			},
			verification(){
				this.onBtnChange()
			}
		},
		methods: {
			// 验证手机号码
			isPhone(){
				let mPattern = /^1[34578]\d{9}$/; 
				return mPattern.test(this.phone);
			},
			// 获取验证码
			getVerification(){
				if(this.codetime > 0){
					uni.showToast({
						title:'不能重复获取',
						icon:'none'
					})
					return 
				}
				// let mPattern = /^1[34578]\d{9}$/; 
				// 验证手机合法性
				// if(!mPattern.test(this.phone)){
				if(!this.isPhone()){
					uni.showToast({
						title:'请输入正确手机号',
						icon:'none'
					})
					return 
				}
				// 请求服务器，发送验证码
				// 发送成功,开启倒计时
				this.codetime =10
				let timer = setInterval(()=>{
					this.codetime--;
					if(this.codetime < 1){
						clearInterval(timer)
						this.codetime = 0
					}
				},1000)
			},
			// 改变按钮状态
			onBtnChange(){
				console.log(this.phone)
				console.log(this.verification)
				if((this.username && this.password)||(this.phone && this.verification)){
					this.disabled = false
					return 
				}
				this.disabled = true
			},
			// 返回上一步
			back(){
				
			},
			// 提交登录
			submit(){
				// 账号密码登录
				if(!this.status){
					
				}else{
					// 手机登录时，验证手机合法性
					if(this.isPhone()){
						uni.showToast({
							title:'请输入正确手机号',
							icon:'none'
						})
						return 
					}
				}
			},
			// 切换登录状态,一旦切换登录状态就清空表单
			changeStatus(){
				this.initInput()
				this.status = !this.status
			},
			// 初始化表单
			initInput(){
				this.username=''
				this.password=''
				this.phone=''
				this.verification=''
			}
		},
		components:{
			uniStatusBar,
			otherLogin
		}
	}
</script>

<style scoped>
	/* 统一样式 */
	.login-padding{ padding:20upx 0}
	.login-font-color{color:#CCCCCC}
	.icon-guanbi{
		position:fixed;
		top:60upx;
		left:30upx;
		font-size:40upx;
		font-weight:bold;
		color:#332F0A;
	}
	.loginhead{
		width:100%;
	}

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
.user-set-btn-disable{
	background-color: #F4F4F4!important;
	border:1upx solid #EEEEEE;
	color:#909090!important;
}
.common-input{
	font-size:30upx;
	border-bottom:1upx solid #F4F4F4;
}

.login-status{
	display:flex;
	justify-content: center;
	align-items:center;
}

.other-login-title{
	display:flex;
	justify-content: center;
	align-items:center;
	position:relative;
}

.other-login-title:before,.other-login-title:after{
	content:'';
	position:absolute;
	background-color: #CCCCCC;
	width:100upx;
	height:1upx;
	top:50%;
}
.other-login-title:before{
	left:25%;
}
.other-login-title:after{
	right:25%;
}

.protocol{
	display:flex;
	justify-content: center;
}

.login-input-box{
	position:relative;
	}
	/* 这里让悬浮的view不会遮盖input输入框内容 */
.login-input-box .forget-input{
	padding-right:150upx;
}
.forget{
	position:absolute;
	right:0;
	top:0;
	height:100%;
	width:150upx;
	display:flex;
	align-items:center;
	justify-content: center;
}

.login-input-box .phone{
	position:absolute;
	left:0;
	top:0;
	height:100%;
	width:100upx;
	display:flex;
	align-items:center;
	justify-content: center;
	font-weight: bold;
}
.login-input-box .phone-input{
	padding-left:100upx;
}

.verification>view{
	background-color: #EEEEEE;
	border-radius: 10upx;
	font-size:25upx;
	width:150upx;
	padding:10upx 0 ;
	display:flex;
	justify-content: center;
	align-items:center;
}
</style>
