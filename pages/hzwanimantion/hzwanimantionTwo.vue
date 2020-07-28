<template>
<view class="notice" style="background-color: #9bf;">
			fegege
			<swiper class="swiper-nav" :circular="true" :vertical="false" :autoplay="true" :interval="1000" :duration="1000" style="background-color: pink;height: 100rpx;">
							<swiper-item style="display: table;" 
							v-for="(item,index) in noticeList" 
							:key="index">
							<view style="width: 100%;height: 100rpx;display: table-cell;vertical-align: middle;" class="right">
							{{item.messageContent}}
							</view>					
							</swiper-item>
						</swiper>
		</view>
</template>
<script>
	export default{
		data() {
			return{
				noticeList:
					[{messageContent:"aaa"},
					{messageContent:"bbb"},
					{messageContent:"ccc"},
					{messageContent:"ddd"},
					]
			}
		},
		methods: {
		}
	}
</script>
<style>
	.notice{
		width: 100%;
		height: 500px;
		display: block;
	}
</style>