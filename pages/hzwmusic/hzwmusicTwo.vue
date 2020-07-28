<template>
	<view class="container">
		<template>
			<zd-uni-header :url_if="url_ifnum"></zd-uni-header>
		</template>
		
		<view class="top_music_word_title" :info="info">
			<text class="top_music_content" :class="current === 0 ? 'top_music_active':'' " @click="top_music">{{musicsong}}</text>
			<text class="top_tit">|</text>
			<text class="top_word_content" :class="current === 1 ? 'top_music_active':'' " @click="top_musicword">{{musicword}}</text>
		</view>
		
		<view class="uni-margin-wrap">
			<swiper :current="current" class="swiper" circular  :autoplay="autoplay" :interval="interval" @change="change" :duration="duration">
				<swiper-item v-for="(item,index) in info" :key="index">
						<view class="swiper-item">
							<view class="">
								<image class="logo" :src="item.src1"></image>
							</view>
							<view class="main_box">
								<view class="box_left">
									<view class="comic_counts comic_padd">
										{{item.comic_count}}
									</view>
									<view class="comic_describes comic_padd">
										{{item.comic_describe}}
									</view>
									<view class="button_box">
										<button class="button_size button_up" type="default">上一首</button>
										<button class="button_size button_middle" type="default">曲目栏</button>
										<button class="button_size button_down" type="default">下一首</button>
									</view>
									<view class="uni-title ">
										<view class="frist-title-left">
										<text>{{music_title}}</text> 
										</view>
									</view>
									<template>
										<zd-uni-music　:reciveMusicInfo="music_infos"></zd-uni-music>
									</template>
								</view>
							</view>
						</view>
				</swiper-item>
				<swiper-item>
					111
				</swiper-item>
			</swiper>
		</view>	

	</view>	
</template>
<script>
	import zdkUniHeader from "../../components/zd-uni-header/zd-uni-header.vue";
	import zdUniMusic from '../../components/zd-uni-music/zd-uni-music.vue';
	export default{
		components:{
			zdkUniHeader,
			zdUniMusic
		},
		data() {
			return {
				music_title:"One-Piece 经典曲",
				musicsong:"歌曲",
				musicword:"歌词",
				url_ifnum:true,
				autoplay: false,
				interval: 3000,
				duration: 500,
				current: 0,
				music_infos:[{
							"musicsrc1":"../../static/timg.jpg",
							"musicsrc2":"../../static/Trangle-icon.png",
							"music_tilte":"910最新曲目",
							"music_content":"あなかさん910",
							"id":1
		},
		{
							"musicsrc1":"../../static/timg.jpg",
							"musicsrc2":"../../static/Trangle-icon.png",
							"music_tilte":"911最新曲目",
							"music_content":"あなかさん911",
							"id":2
		},
		{
							"musicsrc1":"../../static/timg.jpg",
							"musicsrc2":"../../static/Trangle-icon.png",
							"music_tilte":"912最新曲目",
							"music_content":"あなかさん912",
							"id":3
		}],
				info:[{
						src1:'../../static/timg.jpg',
						src3:'../../static/footicon/new.png',
						comic_count:"One-Piece 歌曲1",
						comic_describe:"あなかさん3",
						id:'03'
					}],
				tabBars_act:[
					{
							name:'歌曲',
							id:'gequ'
					},{
							name:'歌词',
							id:'geci'
					}
				]
			}
		},
		onLoad() {
			let str_url = getCurrentPages();
			let mrl = str_url[str_url.length-1];
			// console.log(mrl.route);
			let route_url = mrl.route;
			let split_url = route_url.split('/');
			let get_url = split_url[split_url.length-1];
			console.log(get_url);
		},
		methods: {
			change(e) {
				this.current = e.detail.current;
				// console.log(this.current)
			    },
			top_music() {
				this.current = 0;
			},
			top_musicword() {
				this.current = 1;
			}
		}
	}
</script>

<style>
 /*start swiper */
 .uni-margin-wrap {
	width:100%;
 }
 .swiper {
	height: 1900rpx;
 }
 .logo{
	top: 10rpx;
	height: 512rpx;
	border-radius: 20rpx;
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
	margin:24rpx;
 }
 /*end main_box*/
 
 /*start box_left button_circle */
 .box_left{
	text-align: left;
	color:#FFFFFF;
 }
 .box_left .comic_padd{
	 padding-left:32rpx;
 }
 .box_left .comic_counts{
	font-size: larger;
 }
 .box_left .comic_describes{
	font-size: smaller;
 }
 /*end box_left button_circle */	
	
/*start top_music_word_title */
.top_music_word_title{
	text-align: center;
	text-shadow: 0px 2px 4px black;
	font-weight: 700;
	font-size: 32rpx;
	font-family: "华文宋体","Segoe UI";
	font-style: ;
	color: #D2D2D2;
}
.top_music_active{
	color: #FFFFFF;
}
/*end top_music_word_title */
/*start button_box */
.button_box{
	margin:40rpx auto;
	text-align: center;
	display: flex;
	justify-content:space-around;
}
.button_box .button_size{
	width:180rpx;
	height:60rpx;
	background: radial-gradient(ellipse, #F9BC10 20%, #F86004);
	box-shadow: 0rpx 4rpx 10rpx 4rpx rgba(100,100,100,0.5);
	border:1rpx solid #FFFFFF;
	color: #FFFFFF;
	line-height: 1.45;
}
.button_box .button_up{
	float: left;
}
.button_box .button_middle{
}
.button_box .button_down{
	float: left;
}
/*end button_box */
/*start scroll-frist-title */
.scroll-frist-title{
	margin:12;
	padding-bottom: 28rpx;
 }
 .frist-title-left{
	 float: left;
	 line-height: 0;
	 margin-left: 24rpx;
 }
 .frist-title-left text{
	text-shadow: 0px 2px 4px black;
	font-weight: 700;
	font-size: 36rpx;
	font-family: "Segoe UI";
	font-style: italic;
	color: #FFFFFF;
 }
 /*end scroll-frist-title */
 
 /*start music-autoside-box */
 .music-autoside-box{
	 width: auto !important;
	 margin: 3% auto;
 }
  /*end music-autoside-box */
</style>