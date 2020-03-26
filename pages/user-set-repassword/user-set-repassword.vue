<template>
	<view class='bodybox'>
		<input type="password" v-model='oldpassword'
		class='uni-input common-input'
		 placeholder="输入旧密码">
		 
		<input type="password" v-model='newpassword'
		class='uni-input common-input'
		 placeholder="输入新密码">
		 
		<input type="password" v-model='renewpassword'
		class='uni-input common-input' 
		placeholder="输入确认新密码">
		
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
				oldpassword:'',
				newpassword:'',
				renewpassword:'',
				disabled:true,
				loading:false
			}
		},
		// 通过监听得到,总有一次是三个都有值的
		watch:{
			oldpassword(val){
				this.change()
			},
			newpassword(val){
				this.change()
			},
			renewpassword(val){
				this.change()
			}
		},
		methods: {
			// 监听输入框
			change(){
				if(this.oldpassword && this.newpassword && this.renewpassword){
						this.disabled=false
						return
				}
				this.disabled=true
			},
			// 验证层
			check(){
				if(!this.oldpassword&&this.oldpassword==''){
					uni.showToast({
						title:'旧密码不能为空',
						icon:'none'
					})
					return false
				}
				if(!this.newpassword&&this.newpassword==''){
					uni.showToast({
						title:'请输入新密码',
						icon:'none'
					})
					return false
				}
				if(this.renewpassword!==this.renewpassword){
					uni.showToast({
						title:'确认密码不一致',
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
</style>
