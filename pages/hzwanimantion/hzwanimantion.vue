<template>
	<view class="action">
		<scroll-view class="music_word_box" scroll-y="true" :scroll-top="scrollTop">
			<view class="music_wordcss" id="music_wordid">
				<text v-for="(item,index) in lrcs" :key="index" class="center" :id="item.lrcid">{{item.value}}</text>
				<!-- <text class="right">{{item.time}}</text> -->
			</view>
		</scroll-view>
		
		<view class="uni-padding-wrap">
			<video :src="urls" class="audo-video" @loadedmetadata="loadedmetadata" @timeupdate="timeupdate" controls>
			</video>
			<view class="uni-common-mt">
				<slider 
				:value="currentTime" 
				class="audio-slider"
				activeColor="#FFA200"
				:min="0" 
				:max="duration" 
				@changing="onchanging" 
				@change="onchange"
				/>
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
	const audioUrl = 'http://music.163.com/song/media/outer/url?id=1341454025.mp3';
	export default {
		data() {
			return {
				scrollTop: 0,
				currentLine: 0, //当前播放到哪一句了
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
				music_words:"../../static/love me or him-Ruy.lrc",
				currentTime: 0, //当前进度
				duration: 5000 // 自定义时间长度
			}
		},
		computed: {
			overtimes() {
				return calcTimers(this.currentTime);
			},
			durationtimes() {
				let dur =  calcTimers(this.duration);
				console.log(dur);
				return dur;
			},
			playImage() {
				return this.isPlaying ? "../../static/pause.png" : "../../static/play.png"
			}
		},
		onLoad() {
			this.getLyric(this.music_words);
			this._isChanging = false;
			this._audioContext = null;
			this.createAudio();
		},
		onUnload() {
			if (this._audioContext != null && this.isPlaying) {
				this.stop();
			}
		},
		methods: {
			// scroll: function(e) {
			// 	console.log(e.detail)
			// 	this.old.scrollTop = e.detail.scrollTop
			// },
			getLyric(music_words) {
			   uni.request({
			   	method:'GET',
				url:music_words,
				header:{'content-type': 'text/html'},
			   }).then(result=>{
				   let [err,res] = result;
				   music_words = res.data;
				    this.num = this.splitLyric(music_words);;
			   })
			},
			splitLyric(data) {
				let textlrc = data.split("\n"), 
				//用于匹配时间的正则表达式，匹配的结果类似[xx:xx.xxx]
				// zzlrc = /\[\d{2}:\d{2}.\d{3}\]/g;
				lrc1 = [],
				lrc2 = [],
				lrctime = [],
				lrcword = [],
				zzlrc =/(^\s*)|(\s*$)/g; //去除前后空格
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
			loadedmetadata(data) {
				this.duration = data.detail.duration;
			},
			timeupdate(event) {
				console.log(event.detail)
				let duration ,currenttime;
				currenttime = event.detail.currentTime;
				duration = event.detail.duration;
				this.duration = duration;
				this.currentTime = currenttime;
			},
			createAudio() {
				var innerAudioContext = this._audioContext = uni.createInnerAudioContext();
				innerAudioContext.autoplay = false;
				innerAudioContext.src = audioUrl;
				innerAudioContext.onPlay(() => {
					console.log('开始播放');
				});
				innerAudioContext.onTimeUpdate(() => {
					if (this._isChanging === true) {
						return;
					}
					this.currentTime = innerAudioContext.currentTime || 0;
					//如不另加一个结束时间，到最后歌词滚动不到最后一句
					this.lrctime[this.lrctime.length] = this.lrctime[this.lrctime.length-1] + 3;
					// 删除之前的字幕
					if(this.lrcsecret){
						let clears = document.getElementById(this.lrcsecret);
						clears.classList.remove("onWordredc");
						// console.log(this.currentTime)
					}
					//循环的当前时间 与 现在的当前时间对比
					if(this.lrcsecrettime > this.currentTime){
						this.lrcsecrettime = this.currentTime;
						this.currentLine = 0;
						for(let j=this.currentLine;j<this.lrctime.length; j++){
							if(this.lrcsecrettime < this.lrctime[j+1] && this.lrcsecrettime > this.lrctime[j]){
								this.currentLine = j;
								let lrcnumid = document.getElementById(this.lrcids[j]);
								this.lrcsecret = this.lrcids[j];
								this.lrcsecrettime = this.lrcsecrettime;
								// console.log(this.lrcsecret)
								// 让上一组去掉class，数组里没有负数
								if(j-1 < 0){
									continue;
								}else{
									if(lrcnumid === null){
										return;
									}else{
										let lrcnumid1 = document.getElementById(this.lrcids[j-1]);
										lrcnumid1.classList.remove("onWordredc");
										lrcnumid.classList.add("onWordredc");
									}
									
								};
							}
						}
					}
					for(let j=this.currentLine;j<this.lrctime.length; j++){
						if(this.currentTime < this.lrctime[j+1] && this.currentTime > this.lrctime[j]){
							this.currentLine = j;
							// let ppxx = 250-(this.currentLine*50);
							// let lrclass = document.getElementById("music_wordid");
							// lrclass.style.transform = "translateY("+ppxx+"px)";
							let lrcnumid = document.getElementById(this.lrcids[j]);
							// console.log(lrcnumid.offsetTop);
							this.scrollTop = 52*j;
							this.lrcsecret = this.lrcids[j];
							this.lrcsecrettime = this.currentTime;
							// console.log(this.lrcsecret)
							// 让上一组去掉class，数组里没有负数
							if(j-1 < 0){
								continue;
							}else{
								if(lrcnumid === null){
									return;
								}else{
									let lrcnumid1 = document.getElementById(this.lrcids[j-1]);
									lrcnumid1.classList.remove("onWordredc");
									lrcnumid.classList.add("onWordredc");
								}
								
							};
						}
					}
					this.duration = innerAudioContext.duration || 0;
				});
				innerAudioContext.onSeeked(function(){
					// console.log(this.onWordred)
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
				// console.log(typeof e.detail.value);
				this._audioContext.seek(e.detail.value);
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
			}
		}
	}
	//时间值转化为分、秒
	function calcTimers(Timers) {
		if(Timers === 0 || typeof Timers !== 'number'){
			return '00:00';
		}
		let mm = Math.floor(Timers / 60)
		let ss = Math.floor(Timers % 60)
		// console.log(ss)
		if(mm < 10) {
			mm = '0' + mm
		}
		if(ss < 10) {
			ss = '0' + ss
		}
		// console.log("m+s"+mm+ss)
		return mm + ':' + ss
	}
</script>
<style>
	.action{
		
	}
	.music_word_box{
		white-space: nowrap;
		overflow: hidden;
		height:600rpx;
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
		position: fixed;
		bottom: 100rpx;
	}
	.music_wordcss{
		display: block;
		text-align: center;
		transform: translateY(250px);
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
		margin: -20rpx 40rpx;
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
</style>
