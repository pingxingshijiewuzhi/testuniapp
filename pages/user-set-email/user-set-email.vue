<template>
	<view class='bodybox'>
		<input type="password" v-model='email'
		class='uni-input common-input'
		 placeholder="输入需要绑定的邮箱">
		 
		<input type="password" v-model='password'
		class='uni-input common-input'
		 placeholder="输入密码">

		
		<button class='user-set-btn'
		:class="{'user-set-btn-disable':disabled}"
		:disabled='disabled'
		:loading='loading'
		type='primary' @tap='submit'>完成</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				disabled:true,
				email:'',
				password:'',
				loading:false
			}
		},
		watch:{
			email(val){
				this.change()
			},
			password(val){
				this.change()
			}
		},
		methods: {
			// 监听输入框
			change(){
				if(this.email && this.password){
						this.disabled=false
						return
				}
				this.disabled=true
			},
			// 验证层
			check(){
				if(!this.email&&this.email==''){
					uni.showToast({
						title:'邮箱不能为空',
						icon:'none'
					})
						// 验证邮箱格式
				let ePattern = /^([A-Za-z0-9_\-\.])+\@([A-Za-z0-9_\-\.])+\.([A-Za-z]{2,4})$/;
				if(!ePattern.test(this.email)){
					uni.showToast({
						title: '请输入正确邮箱格式',
						icon:"none"
					});
					return false;
				}
					return false
				}
				if(!this.password&&this.password==''){
					uni.showToast({
						title:'密码不能为空',
						icon:'none'
					})
					return false
				}
				return true
			},
			// 提交更改密码
			submit(){
				this.loading=true
				this.disabled=true
				
				if(!this.check()){this.loading=false;this.disabled=false; return}
				// 提交服务器
				uni.showToast({
					title:'修改成功'
				})
				this.loading=false;
				this.disabled=false;
			}
		}
	}
</script>

<style scoped>
.bodybox{
		padding:0 20upx;
}
.user-set-btn-disable{
	background-color: #F4F4F4!important;
	border:1upx solid #EEEEEE;
	color:#909090!important;
}
.user-set-btn{
	width:100%;
	padding:20upx 0;
	color:#333333!important;
	background-color: #FFE933!important;
	border:0!important;
}
.common-input{
	font-size:30upx;
	border-bottom:1upx solid #F4F4F4;
}
</style>
