<template name="zdUniHeader">
	<view class="header">
		<object data="../../static/title.svg" class="svgStyle" type="image/svg+xml"></object>
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
	.svgStyle{
		width:100%;
		width: 106%;
		margin: 0px -3%;
	}
	/* object svg */
	
	/* title Image */
	.tilteImage{
		width: 150px;
		height: 45px;
		top: -75px;
	}
	/* title Image */
</style>
