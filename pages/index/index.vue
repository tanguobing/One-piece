<template>
	<view class="container">
		<view class="intro">本项目已包含uni ui组件，无需import和注册，可直接使用。在代码区键入字母u，即可通过代码助手列出所有可用组件。光标置于组件名称处按F1，即可查看组件文档。</view>
		<text :class="className" :style="classDemo">详见：</text>
		<text v-if="showBoolean">{{number}}</text>
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
	.container {
		padding: 20px;
		font-size: 14px;
		line-height: 24px;
	}
	.buttonName{
		font-weight: bold;
		color: #ffffff;
		background-color: #007AFF;
	}
	.classNames{
		font-weight:bold;
	}
</style>
