<template name="zdUniScrolltitle">
	<view class="uni-tab-bar">
		<scroll-view id="tab-bar" class="scroll-h" :scroll-x="true" :show-scrollbar="false" :scroll-into-view="scrollInto">
		    <view v-for="(tab,index) in tabBars" :key="tab.id" class="uni-tab-item" :id="tab.id" :data-current="index" @click="ontabtap">
		        <text class="uni-tab-item-title" :class="tabIndex==index ? 'uni-tab-item-title-active' : ''">{{tab.name}}</text>
		    </view>
		</scroll-view>
	</view>
</template>

<script>
	export default{
		name:"zdUniScrolltitle",
		props:["tabBars"],
		data() {
			return{
				
			}
		},
		methods:{
			ontabtap(e) {
			    let index = e.target.dataset.current || e.currentTarget.dataset.current;
			    this.switchTab(index);
			},
		}
	}
</script>
<style scoped>
	
	.uni-tab-bar{
/* 		flex: 1;
		flex-direction: column; */
		overflow: hidden;
		background-color: #ffffff;
		/* #ifdef MP-ALIPAY || MP-BAIDU */
		height: 100vh;
		/* #endif */
	}
	.scroll-h{
		width: 750rpx;
		height: 80rpx;
		/* #ifndef APP-PLUS */
		white-space: nowrap;
		/* #endif */
	}
	.uni-tab-item{
		/* #ifdef APP-PLUS */
		display: inline-block;
		/* #endif */
		/* flex-wrap: nowrap; */
		padding-right: 34rpx;
		padding-left:34rpx;
	}
	
	.uni-tab-item-title {
	    color: #555;
	    font-size: 30rpx;
	    height: 80rpx;
	    line-height: 80rpx;
	    /* flex-wrap: nowrap; */
	    /* #ifndef APP-PLUS */
	    white-space: nowrap;
	    /* #endif */
	}
	
	.uni-tab-item-title:active{
		color: #007AFF;
	}
	
</style>