<template>
	<view class='bodybox'>
		
		<view class="user-set-userinfo-list">
			<view>头像</view>
			<view class="u-f-ac" @tap="changeimg">
				<image :src="userpic" mode="aspectFill" lazy-load></image>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
		<view class="user-set-userinfo-list">
			<view>昵称</view>
			<view class="u-f-ac">
				<!-- text-align: right;来确定输入框始终右侧对齐 -->
				<input type="text" v-model='username'>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
		<view class="user-set-userinfo-list">
			<view>性别</view>
			<view class="u-f-ac" @tap="changeOne('sex')">
				<view>{{sex}}</view>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
		<view class="user-set-userinfo-list">
			<view>生日</view>
			<view class="u-f-ac">
				<picker mode="date" :value="birthday" 
				:start="startDate" :end="endDate"
				 @change="bindDateChange">
				<view>{{birthday}}</view>
				</picker>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
		<view class="user-set-userinfo-list">
			<view>情感</view>
			<view class="u-f-ac" @tap="changeOne('emotion')">
				<view>{{emotion}}</view>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
		<view class="user-set-userinfo-list">
			<view>职业</view>
			<view class="u-f-ac" @tap="changeOne('job')">
				<view>{{job}}</view>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
		<view class="user-set-userinfo-list">
			<view>家乡</view>
			<view class="u-f-ac" @tap="showMulLinkageThreePicker">
				<view>{{pickerText}}</view>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
				
		<button class='user-set-btn'
		type='primary' @tap='submit'>完成</button>
		
		<mpvue-city-picker themeColor="#007AFF" 
		ref="mpvueCityPicker" :pickerValueDefault="cityPickerValueDefault"
		 @onConfirm="onConfirm"></mpvue-city-picker>

	</view>
</template>

<script>
	let sex = ['restrict','male','female']
	let emotion = ['married','signora','bachelordom']
	let job = ['IT','tearcher','husbandman']
	import mpvuePicker from "../../components/mpvue-picker/mpvuePicker.vue"
	export default {
		compontents:{
			mpvuePicker
		},
		data() {
			return {
				userpic:'../../static/图片素材/demo6.jpg',
				username:'fgf',
				sex:'不限',
				emotion:'未婚',
				job:'IT',
				birthday:'93-11-18',
				cityPickerValueDefault: [0, 0, 1],
				pickerText: '江苏-徐州-睢宁',
			}
		},
		computed: {
			startDate() {
				return this.getDate('start');
			},
			endDate() {
				return this.getDate('end');
			}
		},
		onBackPress() {
		  if (this.$refs.mpvueCityPicker.showPicker) {
			this.$refs.mpvueCityPicker.pickerCancel();
			return true;
		  }
		},
		onUnload() {
			if (this.$refs.mpvueCityPicker.showPicker) {
				this.$refs.mpvueCityPicker.pickerCancel()
			}
		},
		methods: {
			// 三级联动
			showMulLinkageThreePicker() {
				this.$refs.mpvueCityPicker.show()
			},
			onConfirm(e) {
				this.pickerText = e.label;
			},
			submit(){
				
			},
			// 修改头像
			changeimg(){
				uni.chooseImage({
				    count: 1, //默认9
				    sizeType: [ 'compressed'], //可以指定是原图还是压缩图，默认二者都有
				    //sourceType: ['album'], //从相册选择
				    success:(res)=>{
				        console.log(JSON.stringify(res.tempFilePaths));
						this.userpic = res.tempFilePaths
				    }
				});
			},
			// 单例选择
			changeOne(val){
				let arr = []
				switch(val){
					case 'sex':
					arr = sex
					break
					case 'emotion':
					arr = emotion
					break
					case 'job':
					arr = job
					break
				}
				uni.showActionSheet({
					itemList:arr,
					success:(res)=>{
						// console.log(res.tapIndex + 1)
						switch(val){
							case 'sex':
							this.sex=arr[res.tapIndex]
							break
							case 'emotion':
							this.emotion=arr[res.tapIndex]
							break
							case 'job':
							this.job = arr[res.tapIndex]
							break
						}
					}
				})
			},
			getDate(type) {
			            const date = new Date();
			            let year = date.getFullYear();
			            let month = date.getMonth() + 1;
			            let day = date.getDate();
			
			            if (type === 'start') {
			                year = year - 60;
			            } else if (type === 'end') {
			                year = year + 2;
			            }
			            month = month > 9 ? month : '0' + month;;
			            day = day > 9 ? day : '0' + day;
			            return `${year}-${month}-${day}`;
			},
			// 修改生日
			bindDateChange(e){
				this.birthday = e.target.value
			},
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


.user-set-userinfo-list{
	display:flex;
	justify-content:space-between;
}
.u-f-ac{
	display:flex;
	align-items:center;
}
.user-set-userinfo-list{
	padding: 20upx;
	border-bottom: 1upx solid #F4F4F4;
}
.user-set-userinfo-list>view:first-child{
	font-size: 32upx;
	font-weight: bold;
	color: #9B9B9B;
}
.user-set-userinfo-list>view:last-child>image{
	width: 80upx;
	height: 80upx;
	border-radius: 100%;
}
.user-set-userinfo-list>view:last-child>input{
	text-align: right;
}
.user-set-userinfo-list>view:last-child>view:last-of-type{
	margin-left: 20upx;
	color: #9B9B9B;
}
</style>
