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
									<!-- <view class="button_box">
										<button class="button_size button_up" type="default">上一首</button>
										<button class="button_size button_middle" type="default">曲目栏</button>
										<button class="button_size button_down" type="default">下一首</button>
									</view> -->
									<!-- <view class="uni-title ">
										<view class="frist-title-left">
										<text>{{music_title}}</text> 
										</view>
									</view>
									<template>
										<zd-uni-music　:reciveMusicInfo="music_infos"></zd-uni-music>
									</template> -->
								</view>
							</view>
						</view>
				</swiper-item>
				<swiper-item>
					<scroll-view class="music_word_box" scroll-y="true" :scroll-top="scrollTop">
							<view class="music_wordcss" id="music_wordid">
								<text v-for="(item,index) in lrcs" :key="index" @click="getCurrentId" :data-num="item.time" :class="{'onWordredc' : classword == item.lrcid}"  ref="contentScr" class="center" :id="item.lrcid">{{item.value}}</text>
							</view>
						</scroll-view>
						
				</swiper-item>
			</swiper>
		</view>	
		<view class="uni-padding-wrap">
			<!-- <video :src="urls" class="audo-video" @loadedmetadata="loadedmetadata" @timeupdate="timeupdate" controls>
			</video> -->
			<view class="uni-common-mt">
				<dc-slider :value="currentTime" 
				class="audio-slider"
				activeColor="#FFA200"
				:min="0" 
				:max="duration" 
				blockColor="#FFe200"
				blockOuterColor= "#FFe200"
				@changing="onchanging" 
				@changed="onchange"></dc-slider>
			</view>
			<view class="uni-common-mt play-time-area">
				<text class="current-time">{{overtimes}}</text>
				<text class="duration">{{durationtimes}}</text>
			</view>
			<view class="play-button-area">
				<image class="icon-play" :src="playImage" @click="play"></image>
			</view>
		</view>
	</view>	
</template>
<script>
	// import jquerys from "../../common/jquery-1.9.1.js";
	import zdkUniHeader from "../../components/zd-uni-header/zd-uni-header.vue";
	import zdUniMusic from '../../components/zd-uni-music/zd-uni-music.vue';
	// import musicUrls from '@/static/7031_4e97_47fb_3900347961cb48a32aaf060577ac7400.mp3';
	import dcSlider from '@/components/ly-drag-slider/dc-slider.vue';
	import musicLrcUrls from '../../common/hzwmusic.js';
	// console.log(musicLrcUrls.data[0].musicurl)
	const audioUrl = musicLrcUrls.data[0].musicurl;
		export default{
		components:{
			zdkUniHeader,
			zdUniMusic,
			dcSlider
		},
		data() {
			return {
				//歌词内容
				classword: '',
				lrcnumid:[],
				scrollTop: 0, //当前滚动高度
				currentLine: 0, //当前播放到哪一句了
				lrcsetStorage: [], //uni.setStorage
				lrcs: [], 
				lrcids: [],
				lrctime: [],
				lrcword: [],
				lrcsecret: "",//存储当前id
				lrcsecrettime: 0,
				num: [],
				title: "innerAudioContext",
				isPlaying: false,
				isPlayEnd: false,
				urls:audioUrl,
				music_words: musicLrcUrls.data[0].test,
				currentTime: 0, //当前进度
				// duration: 5000, // 自定义时间长度
				//歌曲内容
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
		//计算当前歌词内容
		computed: {
			//当前时间
			overtimes() {
				return calcTimers(this.currentTime);
			},
			//歌曲时间
			durationtimes() {
				let dur =  calcTimers(this.duration);
				console.log(dur);
				return dur;
			},
			//按钮控制
			playImage() {
				return this.isPlaying ? "../../static/pause.png" : "../../static/play.png"
			}
		},
		onLoad() {
			//获取自身链接、文件名
			let str_url = getCurrentPages();
			let mrl = str_url[str_url.length-1];
			let route_url = mrl.route;
			let split_url = route_url.split('/');
			let get_url = split_url[split_url.length-1];
			console.log(get_url);
			
			//歌词内容
			this.splitLyric(this.music_words);
			this._isChanging = false;
			this._audioContext = null;
			this.createAudio();
		},
		onUnload() {
			//加载歌词内容
			if (this._audioContext != null && this.isPlaying) {
				this.stop();
			}
		},
		methods: {
			getCurrentId(e) {
				console.log(e.target.dataset.num);
				// let eid = e.target.dataset.num;
				// this._isChanging = false;
				// //this.playing 控制播放图片
				// this.isPlaying = true;
				// this.createAudio(eid);
				// this._audioContext.play();
			},
			// 歌词内容methods
				splitLyric(data) {
					let textlrc = data.split(","),
					//用于匹配时间的正则表达式，匹配的结果类似[xx:xx.xxx]
					// zzlrc = /\[\d{2}:\d{2}.\d{3}\]/g;
					lrc1 = [],
					lrc2 = [],
					lrctime = [],
					lrcword = [],
					zzlrc =/(^\s*)|(\s*$)/g; //去除前后空格
					console.log(textlrc)
					if(textlrc.length == 0)return;
					textlrc.pop();
						for(let i in textlrc){
							if(zzlrc.test(textlrc)){
								textlrc[i] = textlrc[i].replace(zzlrc,""); 
								// 截取时间
								lrc1 = textlrc[i].substring(textlrc[i].indexOf("[") + 1, textlrc[i].indexOf("]"));
								// 截取文字
								lrc2 = textlrc[i].substring(textlrc[i].indexOf("]")+1);
								//00:00.000转化为00:00格式
								lrc1 = parseFloat(lrc1.substr(1,3)) * 60 + parseFloat(lrc1.substring(3,9));
								this.lrctime.push(lrc1);
								this.lrcword.push(lrc2);
							}
						}
					for (let i = 0; i < this.lrctime.length; i++) {
					 let activObject = {};
					 for (let j = 0; j < this.lrcword.length; j++) {
					  if (i == j) {
					   activObject.lrcid = "lrc"+i;
					   activObject.time = this.lrctime[i];
					   activObject.value = this.lrcword[j];
					   this.lrcids.push(activObject.lrcid);
					   this.lrcs.push(activObject);
					  }
					 }
					}
				},
				// loadedmetadata(data) {
				// 	this.duration = data.detail.duration;
				// },
				// timeupdate(event) {
				// 	console.log(event.detail)
				// 	let duration ,currenttime;
				// 	currenttime = event.detail.currentTime;
				// 	duration = event.detail.duration;
				// 	this.duration = duration;
				// 	this.currentTime = currenttime;
				// },
				createAudio() {
					var innerAudioContext = this._audioContext = uni.createInnerAudioContext();
					innerAudioContext.autoplay = false; //介入到此界面是否直接播放
					innerAudioContext.src = audioUrl;
					innerAudioContext.onPlay(() => {
						console.log('开始播放');
					});
					innerAudioContext.onTimeUpdate(() => {
						if (this._isChanging === true) {
							return;
						}
						// console.log(this.lrctime);
						this.currentTime =  innerAudioContext.currentTime || 0;
						//如不另加一个结束时间，到最后歌词滚动不到最后一句
						this.lrctime[this.lrctime.length] = this.lrctime[this.lrctime.length-1] + 3;
						//循环的当前时间 与 现在的当前时间对比
						if(this.lrcsecrettime > this.currentTime){
							this.lrcsecrettime = this.currentTime;
							this.currentLine = 0;
							for(let j=this.currentLine;j<this.lrctime.length; j++){
								if(this.lrcsecrettime < this.lrctime[j+1] && this.lrcsecrettime > this.lrctime[j]){
									this.currentLine = j;
									// this.lrcnumid = this.$refs.contentScr[j].$el;
									this.lrcsecret = this.lrcids[j];
									this.lrcsecrettime = this.lrcsecrettime;
									// 让上一组去掉class，数组里没有负数
									if(j-1 < 0){
										continue;
									}else{
										if(this.lrcsecret === null){
											return;
										}else{
											this.classword = this.lrcsecret;
										}
									}
								}
							}
						}
						for(let j=this.currentLine;j<this.lrctime.length; j++){
							if(this.currentTime < this.lrctime[j+1] && this.currentTime > this.lrctime[j]){
								this.currentLine = j;
								// this.lrcnumid = this.$refs.contentScr[j].$el;
								console.log(this.$refs.contentScr[j])
								this.scrollTop = 50*j;
								this.lrcsecret = this.lrcids[j];
								console.log(this.currentTime)
								this.lrcsecrettime = this.currentTime;
								// 让上一组去掉class，数组里没有负数
								if(j-1 < 0){
									continue;
								}else{
									if(this.lrcsecret === null){
										return;
									}else{
										this.classword = this.lrcsecret;
										console.log(this.classword);
									}
									
								}
							}
						}
						this.duration = innerAudioContext.duration || 0;
					});
					innerAudioContext.onEnded(() => {
						this.currentTime = 0;
						this.isPlaying = false;
						this.isPlayEnd = true;
					});
					innerAudioContext.onError((res) => {
						this.isPlaying = false;
						console.log(res.errMsg);
						console.log(res.errCode);
					});
					return innerAudioContext;
				},
				onchanging() {
					this._isChanging = true;
				},
				onchange(e) {
					this.play();
					console.log(e);
					this._audioContext.seek(e.value);
					this._isChanging = false;
					//this.playing 控制播放图片
					this.isPlaying = true;
					//this.audioContext 控制进度条
					this._audioContext.play();
				},
				play() {
					if (this.isPlaying) {
						this.pause();
						return;
					}
					this.isPlaying = true;
					this._audioContext.play();
					this.isPlayEnd = false;
				},
				pause() {
					this._audioContext.pause();
					this.isPlaying = false;
				},
				stop() {
					this._audioContext.stop();
					this.isPlaying = false;
				},
			
			//歌曲内容methods
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
	//时间值转化为分、秒
	function calcTimers(Timers) {
		if(Timers === 0 || typeof Timers !== 'number'){
			return '00:00';
		}
		let min = Math.floor(Timers / 60)
		let second = Math.floor(Timers % 60)
		// console.log(second)
		if(min < 10) {
			min = '0' + min
		}
		if(second < 10) {
			second = '0' + second
		}
		// console.log("min+s"+min+second)
		return min + ':' + second
	}
</script>

<style>
	/* 歌词内容 */
.music_word_box{
		white-space: nowrap;
		overflow: hidden;
		height:840rpx;
		width: 94%;
		margin: 3%;
}
.onWordredc{
	font-size: 1.2em;
	font-weight: 600;
	background-image: -webkit-linear-gradient(to left,#ffffff 0%, #ff0000 0%);
	background-image: linear-gradient(to left,#ffffff 0% , #ff0000 0%);
	-webkit-background-clip: text;
	-webkit-text-fill-color: transparent;
	animation: font-colors 3s linear normal;
}
@keyframes font-colors{
	0%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 100%);}
	10%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 90%);}
	20%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 80%);}
	30%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 70%);}
	40%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 60%);}
	50%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 50%);}
	60%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 40%);}
	70%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 30%);}
	80%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 20%);}
	90%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 10%);}
	100%{background-image: linear-gradient(to left ,#ffffff 0% , #ff0000 0%);}
}
@-webkit-keyframes font-colors{
	0%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 100%);}
	10%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 90%);}
	20%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 80%);}
	30%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 70%);}
	40%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 60%);}
	50%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 50%);}
	60%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 40%);}
	70%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 30%);}
	80%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 20%);}
	90%{background-image: linear-gradient(to left ,#ffffff 0%, #ff0000 10%);}
	100%{background-image: linear-gradient(to left ,#ffffff 0% , #ff0000 0%);}
}
.uni-padding-wrap{
/* 	position: fixed;
	bottom: 0px; */
}
.music_wordcss{
	display: block;
	text-align: center;
	/* transform: translateY(250px); */
	transform: translateY(0px);
	width: 100%;
	transition-duration: 600ms;
}
.music_wordcss .center{
	color: #FFFFFF;
	overflow: hidden;
	text-overflow: ellipsis;
	height: 25px;
	line-height: 25px;
	-webkit-line-clamp: 1;
	-webkit-box-orient: vertical;
	display: -webkit-box;
	text-align: center;
	margin-top: 0;
	margin-bottom: 25px;
}
.music_wordcss .right{
	float: right;
	border: 1px #000000 solid;
	margin-right: 20rpx;
}
.play-time-area {
	display: flex;
	flex-direction: row;
	font-size: 24rpx;
	/* margin: -20rpx 40rpx; */
}

.duration {
	margin-left: auto;
}

.play-button-area {
	display: flex;
	flex-direction: row;
	justify-content: center;
	margin: 20rpx;
}

.icon-play {
	width: 60px;
	height: 60px;
}
.audo-video{
	display: none;
}
	
 /*start swiper 歌曲内容*/
 .uni-margin-wrap {
	width:100%;
 }
 .swiper {
	height: 840rpx;
	white-space: nowrap;
	overflow: hidden;
	/* height:100%; */
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