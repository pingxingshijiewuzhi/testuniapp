<template>
	<view>
		<view 
		class='viewclass animated '
		hover-class='hover-class-hover bounceIn'
		hover-stay-time=800></view>
		<view class='cssstyle'>
			<view>我是view标签</view>
			<text>文本一\n</text>
			<text>文本er\n</text>
			<text>文本三\n</text>
			<text>文本四\n</text>
		</view>
		<view class='flexbox'>
			<view class='flexbox-item'>1</view>
			<view class='flexbox-item'>2</view>
			<view class='flexbox-item'>3</view>
			<view class='flexbox-item'>4</view>
			<view class='flexbox-item'>5</view>
			<view class='flexbox-item'>6</view>
			<view class='flexbox-item'>7</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>
.viewclass{
	width:200upx;
	height:200upx;
	background-color: #007AFF;
}
.hover-class-hover{
	background-color: red;
}
.cssstyle{
	width:200upx;
	height:400upx;
	background-color: yellow;
}
/* .cssstyle>text:nth-child(1){
	background-color: red;
}
.cssstyle>text:nth-child(4){
	background-color: blue;
} */

.cssstyle>text:nth-child(2n-1){
	background-color: red;
}
.cssstyle>text:nth-child(2n){
	background-color: blue;
}
/* .cssstyle>text:nth-of-type(2n-1){
	background-color: red;
}
.cssstyle>text:nth-of-type(2n){
	background-color: blue;
} */

.flexbox{
	display:flex;
	/* flex-wrap: wrap; */
	/* justify-content:space-between; */
	
	/* 每个元素都是独占一行元素 */
	/* flex-direction: column; */
	
	/* 如果子元素设置高度,则拉伸无效 */
	/* align-items:stretch; */
	
	/* align-items: center; */
	/* justify-content:space-around; */
	/* justify-content:flex-end; */
	/* flex-direction: row; */
	/* flex-grow: 1; */
	height:500upx;
	width:100%;
	border:1upx solid #cccccc
}
.flexbox-item{
	color:#FFFFFF;
	font-size:30upx;
	font-weight:bold;
	height:200upx;
	width:200upx;
	line-height: 200upx;
	text-align: center;
}
.flexbox-item:first-of-type{
	/* 默认值是1,可以被压缩.0是不被压缩 */
	/* 当换行,内容很多菜用到这个元素 */
	/* flex-shrink:0 */
}


.flexbox-item:nth-of-type(odd){
	background:#007AFF;
}
.flexbox-item:nth-of-type(even){
	background:#09BB07;
}
</style>
