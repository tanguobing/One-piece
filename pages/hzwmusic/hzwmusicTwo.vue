<template>
	<view class="container">
		<template>
			<zd-uni-header :url_if="url_ifnum"></zd-uni-header>
		</template>
<!-- 		<view class="top_music_word_title">
			<text class="top_music_content">歌曲</text>
			<text class="top_tit">|</text>
			<text class="top_word_content">歌词</text>
		</view> -->
		<template>
			<zd-uni-scrolltitle :tabBars="tabBars_act"></zd-uni-scrolltitle>
		</template>
	</view>	
</template>
<script>
	import zdkUniHeader from "../../components/zd-uni-header/zd-uni-header.vue";
	import zdUniScrolltitle from "../../components/zd-uni-scrolltitle/zd-uni-scrolltitle.vue";
	export default {
		components:{
			zdkUniHeader,
			zdUniScrolltitle
		},
		data() {
			return {
				url_ifnum:true,
				tabBars_act:[
					{
							name:'歌曲',
							id:'gequ'
					},{
							name:'歌词',
							id:'geci'
					}
				]
			}
		},
		onLoad() {
			let str_url = getCurrentPages();
			let mrl = str_url[str_url.length-1];
			// console.log(mrl.route);
			let route_url = mrl.route;
			let split_url = route_url.split('/');
			let get_url = split_url[split_url.length-1];
			console.log(get_url);
		},
		methods: {
			
		}
	}
</script>

<style>
/*start top_music_word_title */
.top_music_word_title{
	text-align: center;
	text-shadow: 0px 2px 4px black;
	font-weight: 700;
	font-size: 32rpx;
	font-family: "华文宋体","Segoe UI";
	font-style: ;
	color: #FFFFFF;
}

/*end top_music_word_title */
</style>
