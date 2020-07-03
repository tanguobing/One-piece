<template name="zdUniScroll">
	<scroll-view class="scroll-view_H" scroll-x="true" scroll-left="120">
					<view v-for="(item1,index1) in scrollinfo" :key="index1" id="demo1" class="scroll-view-item_H">
						<view class="scroll-logo_box">
							<image class="scroll-logo" :src="item1.scrollsrc1" mode=""></image>
						</view>
						<view class="scroll_view_main">
							<view class="scroll_view_left">
								<view class="scroll_view_tilte">{{item1.scroll_tilte}}</view>
								<view class="scroll_view_content">{{item1.scroll_content}}</view>
							</view>
							<view class="scroll_view_right button_circle">
								<image :src="item1.scrollsrc2" mode=""></image>
							</view>
						</view>
					</view>
	</scroll-view>
</template>
<script>
	export default{
		name:"zdUniScroll",
		props:{
			
		},
		data() {
			return{
				scrollinfo:[{
						scrollsrc1:'../../static/timg.jpg',
						scrollsrc2:'../../static/Trangle-icon.png',
						scroll_tilte:"983话",
						scroll_content:"大联盟的成立3",
					},
					{
						scrollsrc1:'../../static/timg.jpg',
						scrollsrc2:'../../static/Trangle-icon.png',
						scroll_tilte:"982话",
						scroll_content:"大联盟的成立2",
					},
					{
						scrollsrc1:'../../static/timg.jpg',
						scrollsrc2:'../../static/Trangle-icon.png',
						scroll_tilte:"981话",
						scroll_content:"大联盟的成立1",
					}],
			}
		},
		methods:{
			
		}
	}
</script>
<style scoped>
	/*start scroll */
	 .scroll-view_H {
		white-space: nowrap;
		overflow: hidden;
		width: 94%;
		margin: 3%;
		border-radius:3%;
	 }
	 .scroll-view-item_H {
		display: inline-block;
		width: 60%;
		height:100%;
		text-align: center;
		font-size: 36rpx;
		margin-right: 3%;
		border-radius:3%;
		background-color: #FFFFFF;
	 }
	 .scroll-logo_box{
		line-height: 0;
	 }
	 .scroll-logo{
		width:100%;
		height: 350rpx;
		border-radius:3% 3% 0 0;
	 }
	 .scroll_view_main{
		position: relative;
		left: 6rpx;
		bottom:8rpx;
		width:90%;
		padding: 10rpx;
	 }
	 .scroll_view_left{
		float: left;
		text-align: left;
	 }
	 .scroll_view_left .scroll_view_tilte{
		font-size: small;
		font-weight: 600;
	 }
	 .scroll_view_left .scroll_view_content{
		font-size: small;
		line-height: 1;
		color: rgba(0,0,0,0.35);
	 }
	 .scroll_view_right{
		float: right;
		text-align: right;
		width:40rpx;
		height:40rpx;
		padding: 2rpx;
		margin-top: 18rpx;
	 }
	 .scroll_view_right image{
		width:24rpx;
		height:24rpx;
		padding:5rpx;
	 }
	 /*end scroll */
</style>
