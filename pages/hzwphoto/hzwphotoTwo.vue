<template>
	<view class="container">
		<template>
			<zd-uni-header :url_if="url_ifnum"></zd-uni-header>
		</template>
		<view class="photo_show_box">
			<image :src="option_src" :id="option_id" mode=""></image>
			<view class = "photo_content_box">
				{{option_title}}
			</view>
		</view>
	</view>
</template>
<script>
	import zdkUniHeader from "../../components/zd-uni-header/zd-uni-header.vue";
	export default {
		components:{
			zdkUniHeader,
		},
		data() {
			return {
				option_id: "",
				option_src: "",
				option_title: "",
				url_ifnum:true,
			}
		},
		onLoad: function (option) { //option为object类型，会序列化上个页面传递的参数
				console.log(option);
				this.option_id = option.id;
				this.option_src = option.src;
				this.option_title = option.title;
		        console.log(option.id); //打印出上个页面传递的参数。
		        console.log(option.src); //打印出上个页面传递的参数。
		},
		computed: {
		},
		methods: {
	},
	}
</script>
<style>
	.container{
		
	}
	.photo_show_box{
	white-space: nowrap;
	overflow: hidden;
	height:1000rpx;
	width: 96%;
	margin: 2%;
	}
	.photo_show_box image{
	width:100%;
	}
	.photo_content_box{
		text-align: center;
	}
</style>
