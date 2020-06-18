<template>
	<view class="container">
		<text :class="className" :style="classDemo">详见：</text>
		<text v-if="showBoolean">{{number}}</text>
		<image class="logo" src="/static/timg.png"></image>
		<button type="default" :class="buttonType" @click="handleClick">{{showName}}</button>
		<uni-link :href="href" :text="href"></uni-link>
	</view>
</template>

<script>
	export default {
		data() {
			return {
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
			}
		}
	}
</script>

<style>
	.pages-index-index{
		background-color: #E97352;
	}
	.container {
		padding: 20px;
		font-size: 14px;
		line-height: 24px;
	}
	.logo{
		box-shadow: 0px 31px 38px 2px rgba(100,100,100,0.38);
	}
	.buttonName{
		font-weight: bold;
		color: #ffffff;
		background: radial-gradient(circle, #F9CB12,#F9D213, #F85803);
		box-shadow: 0px 2px 10px 4px rgba(100,100,100,0.5);
	}
	.classNames{
		font-weight:bold;
	}
</style>
