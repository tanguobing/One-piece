<template name="zdUniHeader">
	<view class="header">
		<!-- <object data="../../static/title.svg" class="svgStyle" type="image/svg+xml"></object> -->
		<image class="titleImage1" src="../../static/Rectangle-icon.png" mode=""></image>
		<image class="tilteImage" src="../../static/Image-2.png"></image>
	</view>
</template>

<script>
	export default{
		name:"zdUniHeader",
		props:{
		},
		data() {
			return{

			}
		},
		methods:{
			
		}
	}
</script>

<style scoped>
	.header{
		text-align: center;
		height:90px;
	}
	
	/* object svg */
/* 	.svgStyle{
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
	
	/* title Image */
	.tilteImage{
		width: 150px;
		height: 45px;
		top: -75px;
	}
	/* title Image */
</style>
