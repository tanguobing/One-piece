<template name="zdUniMusic">
	<view class="music-autoside-box">
		<view class="music-inside-box" v-for="(item,index) in reciveMusicInfo" :key="index">
			<view class="music-left-box">
				<image :src="item.musicsrc1" mode=""></image>
			</view>
			<view class="music-right-box">
				<view class="music-right-r">
					<view class="music-r-up">{{item.music_tilte}}</view>
					<view class="music-r-down">{{item.music_content}}</view>
				</view>
				<view class="music-right-l button_circle">
					<image :src="item.musicsrc2" mode=""></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		name:"zdUniMusic",
		props:["reciveMusicInfo"],
		data() {
			return{
				
			}
		},
		methods:{
			
		}
	}
</script>
<style scoped>
	/*strat music-autoside-box */
	 .music-autoside-box{
		white-space: nowrap;
		overflow: hidden;
		width: 94%;
		margin: 3%;
	 }
	 .music-inside-box{
		padding: 2%;
		width: 94%;
		height: 158rpx;
		background-color: #FFFFFF;
		border-radius:24rpx;
		margin-bottom: 12rpx;
	 }
	.music-left-box{
		float: left;
	}
	.music-left-box image{
		width: 160rpx;
		height: 160rpx;
		border-radius: 20rpx;
	}
	.music-right-box{
		width:100%;
		height: 160rpx;
	}
	.music-right-box .music-right-r{
		float: left;
		margin-top: 36rpx;
		margin-left: 24rpx;
	}
	.music-right-r .music-r-up{
		color:#000000;
		font-size: unset;
		line-height: 1.2;
	}
	.music-right-r .music-r-down{
		font-size: small;
		color: rgba(0,0,0,0.35);
	}
	.music-right-box .music-right-l{
		float: right;
		text-align: right;
		width:40rpx;
		height:40rpx;
		padding: 2rpx;
		margin-top: 56rpx;
		margin-right:24rpx;
	}
	.music-right-l image{
		width:24rpx;
		height:24rpx;
		padding:5rpx;
	}
	 /*end music-autoside-box */
</style>		