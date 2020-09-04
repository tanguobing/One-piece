<template>
	<view class="container">
		
		<template>
			<zd-uni-header></zd-uni-header>
		</template>
		
		<view class="animant_title_box">
			<view class="animant_tilte_content">
				<uni-search-bar placeholder="搜索图片" radius="100" bgColor="#EEEEEE" @input="input" @confirm="search" />
				<!-- <view class="search-result">cancelButton="auto" clearButton="auto"
					<text class="search-result-text">{{ searchVal }}</text>
				</view> -->
				<view class=""><button type="default">搜索</button></view>
			</view>
		</view>
		
		<template>
			<!-- <navigator url="./hzwanimantTwo" open-type="navigate" hover-class="other-navigator-hover"> -->
			<zd-uni-animant :reciveanimantInfo="animant_info" :animant_if="animant_ifnum"></zd-uni-animant>
			<!-- </navigator> -->
		</template>
		<view class="uni-loadmore" v-if="showLoadMore">{{loadMoreText}}</view>
		
	</view>	
</template>
<script>
	import zdkUniHeader from '../../components/zd-uni-header/zd-uni-header.vue';
	import zdUnianimant from '../../components/zd-uni-animant/zd-uni-animant.vue';
	import animantList from '../../static/json/animant.json';
	console.log();
	export default {
		components:{
			zdkUniHeader,
			zdUnianimant
		},
		data() {
			return {
				res_id:[],
				animant_ifnum: this.res_id ? true : false ,
				animant_info:[],
				loadMoreText: "加载中...",
				showLoadMore: false,
				pagecounts:0,
				max: 0,
				searchVal: '' //搜索
			}
		},
		onLoad() {
			this.initData();
			// this.res_id_fn();
		},
		onUnload() {
			this.max = 0,
			this.animant_info = [],
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
		methods: {
			// res_id_fn() {
			// 	return this.res_id ? false : true
			// },
			//搜索
			search(res) {
				uni.showToast({
					title: '搜索：' + res.value,
					icon: 'none'
				})
			},
			input(res) {
				this.searchVal = res.value
			},
			cancel(res) {
				uni.showToast({
					title: '点击取消，输入值为：' + res.value,
					icon: 'none'
				})
			},
			initData(){
				setTimeout(() => {
					let res_ids = [];
					this.max = 0;
					this.animant_info = [];
					this.max += 5;
					let res = animantList;
					this.pagecounts = res.pagecount;
					console.log(res.pagecount)
					if(res.pagecount < 5){
						for(let i = 0; i < this.max; i++){
							if(res.contents[i] === undefined){
								return false;
							}else{
								this.animant_info = this.animant_info.concat(res.contents[i]);
								console.log(res.contents[i].animantsrc1);
							}
						}
					}else{
						for(let i = this.max-5; i < this.max; i++){
							this.animant_info = this.animant_info.concat(res.contents[i]);
							res_ids.push(res.contents[i].id);
						}
					}
					uni.stopPullDownRefresh();
					this.res_id = res_ids.shift();
				}, 300);
				
			},
			setListData() {
				this.max += 5;
				let res = animantList;
				if(res.contents === "" || res.contents === undefined ){
					return false;
				}
				for(let i = this.max -5; i < this.max; i++){
					if(res.contents[i] === undefined){
						return false;
					}else{
						this.animant_info = this.animant_info.concat(res.contents[i]);
						console.log(res.contents[i].animantsrc1);
					}
				}
			}
	},
	}
</script>
<style>
	.animant_title_box{
		white-space: nowrap;
		overflow: hidden;
		width: 94%;
		margin: 3%;
	}
	.animant_tilte_content{
		border: 1rpx solid red;
		width: 99%;
		height:auto;
	}
	.search-result {
		text-align: left;
		background: #fff;
		padding-left: 39px;
		/* position: absolute; */
		/* width: calc(100% - 65px); */
	}
	
	.search-result-text {
		text-align: center;
		font-size: 14px;
	}
</style>
