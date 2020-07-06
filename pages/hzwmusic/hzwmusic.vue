<template>
	<view class="container">
		<template>
			<zd-uni-header :url_if="url_ifnum"></zd-uni-header>
		</template>
	
	
	<view class="uni-title scroll-frist-title">
		<view class="frist-title-left">
		<text>{{music_title}}</text> 
		<image src="../../static/footicon/new.png" mode=""></image>
		</view>
	</view>
	
	<view class="music-autoside-box" scroll-x="true" scroll-left="120">
		<navigator url="./hzwmusicTwo" open-type="redirect" hover-class="other-navigator-hover">
		<view class="music-inside-box" v-for="(item1,index1) in musicinfo" :key="index1">
			<view class="music-left-box">
				<image :src="item1.musicsrc1" mode=""></image>
			</view>
			<view class="music-right-l button_circle">
				<image :src="item1.musicsrc2" mode=""></image>
			</view>
			<view class="music-right-box">
					<view class="music-r-content">{{item1.music_content}}</view>
			</view>
		</view>
		</navigator>
	</view>
	
	<view class="uni-title scroll-frist-title">
		<view class="frist-title-left">
		<text>{{music_title1}}</text> 
		<image src="../../static/footicon/new.png" mode=""></image>
		</view>
	</view>
	
	<template>
		<zd-uni-music　:reciveMusicInfo="music_info"></zd-uni-music>
	</template>
	
	<view class="uni-loadmore" v-if="showLoadMore">{{loadMoreText}}</view>
	</view>
</template>

<script>
	import zdkUniHeader from '../../components/zd-uni-header/zd-uni-header.vue';
	import zdUniMusic from '../../components/zd-uni-music/zd-uni-music.vue';
	export default{
		components:{
			zdkUniHeader,
			zdUniMusic
		},
		data(){
			return{
				url_ifnum:false,
				music_title:"One-Piece 经典曲",
				music_title1:"One-Piece 歌曲",
				loadMoreText: "加载中...",
				showLoadMore: false,
				pagecounts:0,
				max: 0,
				musicinfo:[{
						musicsrc1:'../../static/timg (2).jpg',
						musicsrc2:'../../static/Trangle-icon.png',
						music_content:"あなかさん3",
					},
					{
						musicsrc1:'../../static/timg (2).jpg',
						musicsrc2:'../../static/Trangle-icon.png',
						music_content:"あなかさん2",
					},
					{
						musicsrc1:'../../static/timg (2).jpg',
						musicsrc2:'../../static/Trangle-icon.png',
						music_content:"あなかさん1",
					}],
				music_info:[]
			}
		},
		onLoad() {
			let str_url = getCurrentPages();
			let mrl = str_url[str_url.length-1];
			// console.log(mrl.route);
			let route_url = mrl.route;
			console.log(route_url)
			this.initData();
		},
		onUnload() {
			this.max = 0,
			this.music_info = [],
			this.loadMoreText = "加载更多",
			this.showLoadMore = false;
		},
		onReachBottom() {
			console.log("onReachBottom");
			if (this.max > this.pagecounts) {
				this.loadMoreText = "没有更多数据了!"
				return;
			}
			this.showLoadMore = true;
			setTimeout(() => {
				this.setListData();
			}, 300);
		},
		onPullDownRefresh() {
			console.log('onPullDownRefresh');
			this.initData();
		},
		methods:{
		initData(){
			setTimeout(() => {
				this.max = 0;
				this.music_info = [];
				this.max += 5;
				uni.request({
							url:'../../static/json/hzwmusic.json',
							}).then(result=>{
							let [err,res]=result;
							this.pagecounts = res.data.pagecount;
							console.log(res.data.pagecount)
							if(res.data.pagecount < 5){
								for(let i = 0; i < this.max; i++){
									if(res.data.contents[i] === undefined){
										return false;
									}else{
										this.music_info = this.music_info.concat(res.data.contents[i]);
										console.log(res.data.contents[i].id);
									}
								}
							}else{
								for(let i = this.max-5; i < this.max; i++){
									this.music_info = this.music_info.concat(res.data.contents[i]);
								}
							}
							})
				
				uni.stopPullDownRefresh();
			}, 300);
		},
		setListData() {
			this.max += 5;
			uni.request({
				url:'../../static/json/hzwmusic.json',
			}).then(result=>{
			let [err,res]=result;
				if(res.data.contents === "" || res.data.contents === undefined ){
					return false;
				}
				for(let i = this.max -5; i < this.max; i++){
					if(res.data.contents[i] === undefined){
						return false;
					}else{
						this.music_info = this.music_info.concat(res.data.contents[i]);
						console.log(res.data.contents[i].id);
					}
						
				}
			});
		}	
		}
	}
</script>
<style>
/*start scroll-frist-title */
 .scroll-frist-title{
	margin:0% 3%;
	padding-bottom: 28rpx;
 }
 .frist-title-left{
	 float: left;
	 line-height: 0;
 }
 .frist-title-left text{
	text-shadow: 0px 2px 4px black;
	font-weight: 700;
	font-size: 36rpx;
	font-family: "Segoe UI";
	font-style: italic;
	color: #FFFFFF;
 }
 .scroll-frist-title image{
	width: 1.5em;
	height: .8em;
	left: 12rpx;
	top: 8rpx;
 }
 /*end scroll-frist-title */	
 
/*strat music-autoside-box */
  .music-autoside-box{
 	white-space: nowrap;
 	overflow: hidden;
 	width: 94%;
 	margin: 3%;
  }
  .music-inside-box{
	float: left;
	width: 31%;
	height: 100%;
	/* background-color: #FFFFFF; */
	border-radius: 24rpx;
	margin: 1%;
  }
 .music-left-box{
	
 }
 .music-left-box image{
 	width: 100%;
 	height: 220rpx;
 	border-radius: 20rpx;
 }
 .music-right-box{
	position: relative;
	text-align: left;
	margin-top: -44rpx;
 }
 .music-r-content{
 	font-size: smaller;
 	color: rgb(255, 255, 255);
 	line-height: 1.2;
	margin-right: 8rpx;
	text-overflow: ellipsis;
	overflow: hidden;
 }
 .music-right-l{
 	text-align: right;
 	width:40rpx;
 	height:40rpx;
 	padding: 2rpx;
	margin-right: 8rpx;
	position: relative;
	bottom: 68rpx;
	left: 20rpx;
 }
 .music-right-l image{
 	width:24rpx;
 	height:24rpx;
 	padding:5rpx;
 }
  /*end music-autoside-box */
  
</style>
		