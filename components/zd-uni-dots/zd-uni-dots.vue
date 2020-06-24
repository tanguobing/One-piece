// swiperDot.vue

<template>
	<view class="dot-main">
		<view :class="['dot-item',current==index?'active':'']" v-for="(item,index) in list" :key="index"></view>
	</view>
</template>
<style>
	.dot-main {
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.dot-item {
		width: 80rpx;
		height: 10.41rpx;
		/* border-radius: 50%; */
		background-color: #f86a05;
		margin: 0 6upx;
		box-sizing: border-box;
	}
	.active {
		background-color: #f9ce12;
	}
</style>
<script>
	export default {
		props: [ 'list','current'],
		data() {
			return {
				
			};
		}
	}
</script>
