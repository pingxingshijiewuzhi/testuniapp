<script>
	export default {
		onLaunch: function() {
			// 还用检验全局方法注册吗？
			// console.log(this.config.webUrl)
			this.lib.NetWork.On();
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	/* 通过新建一个项目,从新建样板中复制过来 */
	/* 引入官方css库 */
	 @import './common/uni.css';
	 /* 引入自定义图标库 */
	 @import './common/icon.css';
	 /* 下面这是主要图标库来源,我的阿里图标库没有这个文件 */
	 @import './static/阿里矢量图标/aliiconfont.css';
	 /* 引入animated动画库样式 */
	 @import './common/animate.min.css';
	 
</style>
