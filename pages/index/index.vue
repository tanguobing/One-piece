<template>
	<view class="container">
		<image class="" src="/static/one-piece2.png"></image>
		
		<!-- <text :class="className" :style="classDemo">详见：</text> -->
		
		<!-- <text v-if="showBoolean">{{number}}</text> -->
		
		<!-- <object data="/static/title.svg" type="image/svg+xml"></object> -->
		
		<view class="uni-margin-wrap">
			<swiper class="swiper" circular :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
				<swiper-item>
					<view class="swiper-item">
						<image class="logo" src="/static/timg.png"></image>
					</view>
				</swiper-item>
				<swiper-item>
					<view class="swiper-item ">B</view>
				</swiper-item>
				<swiper-item>
					<view class="swiper-item ">C</view>
				</swiper-item>
			</swiper>
		</view>
		
		
		<view class="swiper-list">
			<view class="uni-list-cell uni-list-cell-pd">
				<view class="uni-list-cell-db">指示点</view>
				<switch :checked="indicatorDots" @change="changeIndicatorDots" />
			</view>
			<view class="uni-list-cell uni-list-cell-pd">
				<view class="uni-list-cell-db">自动播放</view>
				<switch :checked="autoplay" @change="changeAutoplay" />
			</view>
		</view>
		
		<view class="uni-padding-wrap">
			<view class="uni-common-mt">
				<text>幻灯片切换时长(ms)</text>
				<text class="info">{{duration}}</text>
			</view>
			<slider @change="durationChange" :value="duration" min="500" max="2000" />
			<view class="uni-common-mt">
				<text>自动播放间隔时长(ms)</text>
				<text class="info">{{interval}}</text>
			</view>
			<slider @change="intervalChange" :value="interval" min="2000" max="10000" />
		</view>
		
		<!-- <button type="default" :class="buttonType" @click="handleClick">{{showName}}</button> -->
		
		<!--<uni-link :href="href" :text="href"></uni-link>-->
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				background: ['color1', 'color2', 'color3'],
				indicatorDots: true,
				autoplay: true,
				interval: 2000,
				duration: 500,
				className:'classNames',
				showBoolean:'true',
				showName:"隐藏",
				buttonType:"buttonName",
				classDemo: {background:'red'},
				number: 758758,
				href: 'https://uniapp.dcloud.io/component/README?id=uniui'
			}
		},
		methods: {
			handleClick() {
				this.showBoolean = !this.showBoolean;
				this.showName = this.showBoolean ? "显示":"隐藏";
			},
			changeIndicatorDots(e) {
					this.indicatorDots = !this.indicatorDots
				},
				changeAutoplay(e) {
					this.autoplay = !this.autoplay
				},
				intervalChange(e) {
					this.interval = e.detail.value
				},
				durationChange(e) {
					this.duration = e.detail.value
				}
			}
	}
</script>

<style>
	.container {
		/* padding: 20px; */
		font-size: 14px;
		line-height: 24px;
	}
	/* swiper */
	.uni-margin-wrap {
		width:100%;
		background-color: #FFFFFF;
		/* margin:0 30rpx; */
	}
	.swiper {
		height: 600rpx;
	}
	.swiper-item {
		display: block;
		height: 300rpx;
		line-height: 300rpx;
		text-align: center;
	}
	/* swiper */
	.logo{
		box-shadow: 0px 31px 38px 2px rgba(100,100,100,0.38);
	}
	.buttonName{
		font-weight: bold;
		color: #FFFFFF;
		background: radial-gradient(circle, #F9CB12,#F9D213, #F85803);
		box-shadow: 0px 2px 10px 4px rgba(100,100,100,0.5);
	}
	.classNames{
		font-weight:bold;
	}
</style>
