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
		
		<view class="uni-title uni-common-mt scroll-frist-title">
			<view class="frist-title-left">
			<text>{{scroll_title}}</text> 
			<image src="../../static/footicon/new.png" mode=""></image>
			</view>
			<view class="frist-title-right">
				<navigator url="../hzwanimantion/hzwanimantion" open-type="switchTab" >
				<text>更多</text>
				</navigator>
			</view>
		</view>
		
		<template>
			<zd-uni-scroll></zd-uni-scroll>
		</template>
		
		<view class="uni-title uni-common-mt scroll-frist-title">
			<view class="frist-title-left">
			<text>{{music_title}}</text> 
			<image src="../../static/footicon/new.png" mode=""></image>
			</view>
			<view class="frist-title-right">
				<navigator url="../hzwmusic/hzwmusic" open-type="switchTab" >
				<text>更多</text>
				</navigator>
			</view>
		</view>
		
		<template>
			<zd-uni-music :reciveMusicInfo="music_info"></zd-uni-music>
		</template>
		
		<view class="uni-title uni-common-mt scroll-frist-title">
			<view class="frist-title-left">
			<text>{{picture_title}}</text> 
			<image src="../../static/footicon/new.png" mode=""></image>
			</view>
			<view class="frist-title-right">
				<navigator url="../hzwphoto/hzwphoto" open-type="switchTab" >
				<text>更多</text>
				</navigator>
			</view>
		</view>
		
		<view>
			<scroll-view class="picture-view_H" scroll-x="true" scroll-left="120">
				<view v-for="(item3,index3) in pictureinfo" :key="index3" id="demo3" class="picture-view-item_H">
					<view class="picture-logo_box">
						<image class="picture-logo" :src="item3.picturesrc1" mode=""></image>
						<view class="picture_view button_circle">
							<image :src="item3.picturesrc2" mode=""></image>
						</view>
					</view>
					<view class="picture_view_main">
						<text class="picture_view_content">{{item3.picture_content}}</text>
					</view>
				</view>
			</scroll-view>
		</view>
		
		<view class="uni-title uni-common-mt scroll-frist-title">
			<view class="frist-title-left">
			<text>{{comic_title}}</text> 
			<image src="../../static/footicon/new.png" mode=""></image>
			</view>
			<view class="frist-title-right">
				<navigator url="../hzwcomic/hzwcomic" open-type="switchTab" >
				<text>更多</text>
				</navigator>
			</view>
		</view>
		
		<view class="comic-autoside-box" scroll-x="true" scroll-left="120">
			<view class="comic-inside-box" v-for="(item4,index4) in comicinfo" :key="index4">
				<view class="comic-left-box">
					<image :src="item4.comicsrc1" mode=""></image>
				</view>
				<view class="comic-right-box">
					<view class="comic-right-r">
						<view class="comic-r-content">{{item4.comic_content}}</view>
					</view>
					<view class="comic-right-l button_circle">
						<image :src="item4.comicsrc2" mode=""></image>
					</view>
				</view>
			</view>
		</view>
		
	</view>
</template>
<script>
	import zdkUniHeader from '../../components/zd-uni-header/zd-uni-header.vue';
	import uniSwiperDot from "@/components/uni-swiper-dot/uni-swiper-dot.vue";
	import zdUniScroll from '../../components/zd-uni-scroll/zd-uni-scroll.vue';
	import zdUniMusic from '../../components/zd-uni-music/zd-uni-music.vue';
	export default {
		components:{
			zdkUniHeader,
			uniSwiperDot,
			zdUniScroll,
			zdUniMusic
		},
		data() {
			return {
				scroll_title:"动漫",
				music_title:"音乐",
				picture_title:"图片",
				comic_title:"漫画",
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
				music_info:[{
						musicsrc1:'../../static/timg.jpg',
						musicsrc2:'../../static/Trangle-icon.png',
						music_tilte:"最新曲目3",
						music_content:"あなかさん3",
					},
					{
						musicsrc1:'../../static/timg.jpg',
						musicsrc2:'../../static/Trangle-icon.png',
						music_tilte:"最新曲目2",
						music_content:"あなかさん2",
					},
					{
						musicsrc1:'../../static/timg.jpg',
						musicsrc2:'../../static/Trangle-icon.png',
						music_tilte:"最新曲目1",
						music_content:"あなかさん1",
					}],
				pictureinfo:[{
						picturesrc1:'../../static/timg.jpg',
						picturesrc2:'../../static/Shape.png',
						picture_content:"大联盟的成立2",
					},
					{
						picturesrc1:'../../static/timg.jpg',
						picturesrc2:'../../static/Shape.png',
						picture_content:"大联盟的成立2",
					},
					{
						picturesrc1:'../../static/timg.jpg',
						picturesrc2:'../../static/Shape.png',
						picture_content:"大联盟的成立1",
					}],
				comicinfo:[{
						comicsrc1:'../../static/timg.jpg',
						comicsrc2:'../../static/Trangle-icon.png',
						comic_content:"983话3",
					},
					{
						comicsrc1:'../../static/timg.jpg',
						comicsrc2:'../../static/Trangle-icon.png',
						comic_content:"983话2",
					},
					{
						comicsrc1:'../../static/timg.jpg',
						comicsrc2:'../../static/Trangle-icon.png',
						comic_content:"983话1",
					},
					{
						comicsrc1:'../../static/timg.jpg',
						comicsrc2:'../../static/Trangle-icon.png',
						comic_content:"983话0",
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
 
 /*start scroll-frist-title */
 .scroll-frist-title{
	margin: 5%;
 }
 .frist-title-left{
	 float: left;
 }
 .frist-title-left text{
	font-weight: 600;
	font-size: 36rpx;
	color: #FFFFFF;
 }
 .scroll-frist-title image{
	width: 1.5em;
	height: .8em;
	left: 12rpx;
	top: 8rpx;
 }
 .frist-title-right{
	float: right;
	margin-top: 4rpx;
 }
 .frist-title-right text{
	font-size: 24rpx;
	color: #e97352;
	background: #fff;
	border-radius: 30rpx;
	padding: 4rpx 24rpx;
 }
 /*end scroll-frist-title */
 
 /*start picture */
 .picture-view_H {
 	white-space: nowrap;
 	overflow: hidden;
 	width: 94%;
 	margin: 3%;
 	border-radius:3%;
 }
 .picture-view-item_H {
 	display: inline-block;
 	width: 33%;
 	height: 100%;
 	text-align: center;
 	font-size: 17px;
 	margin-right: 3%;
 	border-radius: 6% 6%;
 	background-color: #FFFFFF;
 }
 .picture-logo_box{
 	line-height: 0;
 }
 .picture-logo{
 	width: 100%;
 	height: 236rpx;
 	border-radius: 6% 6% 0 0;
 }
 .picture_view_main{
 	position: relative;
 	left: 6rpx;
 	margin-top: 84rpx;
	margin-bottom: 20rpx;
 }
.picture_view_content{
 	font-size: smaller;
 	line-height: 1;
 	color: rgba(0,0,0,0.35);
 }
 .picture_view{
 	width:40rpx;
 	height:40rpx;
 	padding: 2rpx;
 	margin: -54rpx 20rpx;
	position: relative;
	z-index: 2;
	background:rgba(158, 49, 62,0.55);
 }
 .picture_view image{
 	width:28rpx;
 	height:26rpx;
 	padding:6rpx;
 }
 /*end picture */
 
 /*strat comic-autoside-box */
  .comic-autoside-box{
 	white-space: nowrap;
 	overflow: hidden;
 	width: 94%;
 	margin: 3%;
  }
  .comic-inside-box{
	float:left;
 	padding: 2%;
 	width: 44%;
 	height: 291rpx;
 	background-color: #FFFFFF;
 	border-radius:24rpx;
 	margin-bottom: 10rpx;
	margin: 1%;
  }
 .comic-left-box{

 }
 .comic-left-box image{
 	width: 100%;
 	height: 291rpx;
 	border-radius: 20rpx;
 }
 .comic-right-box{
	position: relative;
	margin: -64rpx auto;
 }
 .comic-right-box .comic-right-r{
 	float: left;
	margin-left: 8rpx;
 }
 .comic-right-r .comic-r-content{
 	font-size: small;
 	color: rgb(255, 255, 255);
 	line-height: 1.2;
	margin-right: 8rpx;
 }
 .comic-right-box .comic-right-l{
 	float: right;
 	text-align: right;
 	width:40rpx;
 	height:40rpx;
 	padding: 2rpx;
	margin-right: 8rpx;
 }
 .comic-right-l image{
 	width:24rpx;
 	height:24rpx;
 	padding:5rpx;
 }
  /*end comic-autoside-box */
</style>
