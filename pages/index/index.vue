<template>
	<view class="container">
		<template>
			<zdkUniHeader></zdkUniHeader>
		</template>
		
		<view class="uni-margin-wrap">
			<uniSwiperDot :info="info" :current="current" field="content" :mode="mode">
			<swiper class="swiper" circular  :autoplay="autoplay" :interval="interval" @change="change" :duration="duration">
				<swiper-item v-for="(item,index) in info" :key="index">
					<view class="swiper-item">
						<view class="">
							<image class="logo" :src="item.src1"></image>
						</view>
						<view class="main_box">
							<view class="box_right">
								<image class="button_circle icon_size" :src="item.src2" mode=""></image>
							</view>
							<view class="box_left">
								<view class="new_s">
									<image :src="item.src3" mode=""></image>
								</view>
								<view class="comic_counts">
									{{item.comic_count}}
								</view>
								<view class="comic_describes">
									{{item.comic_describe}}
								</view>
							</view>
						</view>
					</view>
				</swiper-item>
			</swiper>
			</uniSwiperDot>
		</view>
		
		<!--<uni-link :href="href" :text="href"></uni-link>-->
		
		<view class="uni-title uni-common-mt">
			<view class="" >
			{{tiltess}}
			
			</view>
		</view>
		<view>
			<scroll-view class="scroll-view_H" scroll-x="true" scroll-left="120">
				<view id="demo1" class="scroll-view-item_H uni-bg-red">
					<view class="">
						<image class="scroll-logo" src="../../static/timg (2).jpg" mode=""></image>
					</view>
					<view class="scroll_view_main">
						<view class="scroll_view_left">
							<view class="scroll_view_tilte">983话</view>
							<view class="scroll_view_content">大联盟的成立3</view>
						</view>
						<view class="scroll_view_right">
							<image src="../../static/footicon/Triangle.png" mode=""></image>
						</view>
					</view>
				</view>
				<view id="demo2" class="scroll-view-item_H uni-bg-green">B</view>
				<view id="demo3" class="scroll-view-item_H uni-bg-blue">C</view>
				<view id="demo4" class="scroll-view-item_H uni-bg-green">D</view>
				<view id="demo5" class="scroll-view-item_H uni-bg-red">F</view>
			</scroll-view>
		</view>
		<view class="uni-common-pb"></view>
		
	</view>
</template>
<script>
	import zdkUniHeader from '../../components/zd-uni-header/zd-uni-header.vue';
	import uniSwiperDot from "@/components/uni-swiper-dot/uni-swiper-dot.vue";
	export default {
		components:{
			zdkUniHeader,
			uniSwiperDot
		},
		data() {
			return {
				tiltess:"标题",
				mode:"default",
				current: 0,
				info:[{
						src1:'../../static/timg.jpg',
						src2:'../../static/Bookmark-icon.png',
						src3:'../../static/footicon/new.png',
						comic_count:"983话",
						comic_describe:"大联盟的成立3",
					},
					{
						src1:'/static/timg (2).jpg',
						src2:'../../static/Bookmark-icon.png',
						src3:'../../static/footicon/new.png',
						comic_count:"982话",
						comic_describe:"大联盟的成立2",
					},
					{
						src1:'/static/timg.jpg',
						src2:'../../static/Bookmark-icon.png',
						src3:'../../static/footicon/new.png',
						comic_count:"981话",
						comic_describe:"大联盟的成立1",
					}],
				background: ['color1', 'color2', 'color3'],
				indicatorDots: true,
				autoplay: true,
				interval: 3000,
				duration: 1500,
				scrollTop: 0,
				old: {
					scrollTop: 0
				}
				//href: 'https://uniapp.dcloud.io/component/README?id=uniui'
			}
		},
		methods: {
			 change(e) {
			            this.current = e.detail.current;
			     },
			}
	}
</script>

<style>
	.container {
		font-size: 14px;
		line-height: 24px;
	}
	
	/*start swiper */
	.uni-margin-wrap {
		width:100%;
		background-color: #FFFFFF;
	}
	.swiper {
		height: 630rpx;
	}
	.logo{
		box-shadow: 0px 19px 35px 2px rgba(100,100,100,0.38);
		top: 20px;
		height: 185px;
	}
	.swiper-item {
		height: 600rpx;
		text-align: center;
		position: relative;
		top: 0;
		right: 0;
	}
	/*end swiper */
	
	/*start main_box */
	.main_box{
		margin:2.2em;
	}
	/*end main_box*/
	
	/*start box_right new_s comic_describe comic_counts*/
	.box_right{
		float: right;
	}
	.box_right .button_circle{
		width: 100rpx;
		height: 100rpx;
		border-radius: 60rpx;
		background: rgba(158,49,62,0.45);
		box-shadow: 0px 10px 24px 1px rgba(158,49,62,0.27);
	}
	.box_right .icon_size{
		width:60rpx;
		height:60rpx;
		padding: 12rpx;
	}
	/*end box_right new_s comic_describe comic_counts*/
	
	/*start box_left button_circle */
	.box_left{
		float: left;
		text-align: left;
	}
	.box_left .new_s image{
		width: 2em;
		height: 1em;
		line-height: 1.2;
	}
	.box_left .comic_counts{
		color:#000000;
		font-size: large;
		line-height: 1.2;
	}
	.box_left .comic_describes{
		color: rgba(0,0,0,0.35);
		font-size: small;
	}
	/*end box_left button_circle */
	
	/*start scroll */
	.scroll-view_H {
		white-space: nowrap;
		overflow: hidden;
		background-color: #FFFFFF;
		width: 700rpx;
		margin: 3%;
		border-radius: 2%;
	}
	.scroll-view-item_H {
		display: inline-block;
		width: 30%;
		height: 300rpx;
		line-height: 300rpx;
		text-align: center;
		font-size: 36rpx;
		margin-right: 1%;
	}
	.scroll-logo{
		width:100%;
		height: 82px;
	}
	.scroll_view_main{
		
	}
	.scroll_view_left{
		float: left;
	}
	.scroll_view_left .scroll_view_tilte{
		
	}
	.scroll_view_left .scroll_view_content{
		
	}
	.scroll_view_right{
		float: right;
	}
	.scroll_view_right image{
		width:30rpx;
		height:30rpx;
	}
	/*end scroll */
</style>
