<template name="zdUniHeader">
	<view class="header" v-if="url_if">
		<!-- <button type="default">{{url_if}}</button> -->
		<!-- <object data="../../static/title.svg" class="svgStyle" type="image/svg+xml"></object> -->
		<image class="titleImage1" src="../../static/Rectangle-icon.png" mode=""></image>
		<image class="tiltereturn" src="../../static/footicon/return.png" @click="navigateBack" mode=""></image>
		<image class="tilteImage" src="../../static/Image-2.png"></image>
	</view>
	<view class="header" v-else>
		<image class="titleImage1" src="../../static/Rectangle-icon.png" mode=""></image>
		<image class="tilteImage-1" src="../../static/Image-2.png"></image>
	</view>
</template>

<script>
	export default{
 name:"zdUniHeader",
 props:["url_if"],
		data() {
			return{
			}
		},
		onLoad() {
			console.log(this.url_if);
		},
 methods:{
			navigateBack() {
				uni.navigateBack(0);
			}
		}
	}
</script>

<style scoped>
	.header{
		text-align: center;
		height:150rpx;
	}
	
	/* object svg */
/* .svgStyle{
 width:100%;
 width: 106%;
 margin: 0px -3%;
	} */
	/* object svg */
	
	/* tilteImage1 */
	.titleImage1{
		width:105%;
		height:160rpx;
		margin:0px -3%;
	}
	/* titleImage1 */
	
	/* tilteImage-1 */
	.tilteImage-1{
		width: 300rpx;
		height: 90rpx;
		top: -156rpx;
	}
	/* tilteImage-1 */
	
	/* title Image */
	.tilteImage{
		width: 300rpx;
		height: 90rpx;
		top: -202rpx;
	}
	/* title Image */
	
	/* tiltereturn */
	.tiltereturn{
		width: 60rpx;
		height: 52rpx;
		top: -120rpx;
		left:16rpx;
		display: table-cell;
	}
	/* tiltereturn */
</style>