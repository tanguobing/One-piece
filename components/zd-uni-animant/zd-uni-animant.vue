<template name="zdUnianimant">
	<view class="animant-autoside-box" v-if="animant_if">
		<view class="animant-inside-box" v-for="(item,index) in reciveanimantInfo" :id="item.id" :key="index" @click="navigators">
			<view class="animant-left-box">
				<image :src="item.animantsrc1" mode=""></image>
			</view>
			<view class="animant-right-box">
				<view class="animant-right-r">
					<view class="animant-r-up">{{item.animant_title}}</view>
					<view class="animant-r-down">{{item.animant_content}}</view>
				</view>
				<view class="animant-right-l button_circle">
					<image :src="item.animantsrc2" mode=""></image>
				</view>
			</view>
		</view>
	</view>
	<view class="animant-autoside-box" v-else>
		<view class="animant-inside-box" v-for="(item,index) in reciveanimantInfo" :id="item.id" :key="index" @click="navigators">
			<view class="animant-left-box">
				<image :src="item.animantsrc1" mode=""></image>
			</view>
			<view class="animant-right-box">
				<view class="animant-right-r">
					<image :src="item.animant_newtip" mode=""></image>
					<view class="animant-r-up">{{item.animant_title}}</view>
					<view class="animant-r-down">{{item.animant_content}}</view>
				</view>
				<view class="animant-right-l button_circle">
					<image :src="item.animantsrc2" mode=""></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{ 
		name:"zdUnianimant",
		props:["reciveanimantInfo","animant_if"],
		data() {
			return{
			}
		},
		methods:{
			navigators(e){
				let currentTargetid = Number(e.currentTarget.id);
				let reciveanimantInfo_id,reciveanimantInfo_animantsrc1,reciveanimantInfo_animant_title;
				console.log(typeof currentTargetid);
				for(let i = 0; i < this.reciveanimantInfo.length;i++){
					if(currentTargetid === this.reciveanimantInfo[i].id){
						reciveanimantInfo_id = this.reciveanimantInfo[i].id;
						reciveanimantInfo_animantsrc1 = this.reciveanimantInfo[i].animantsrc1;
						reciveanimantInfo_animant_title = String(this.reciveanimantInfo[i].animant_title);
					}
				}
				 uni.navigateTo({
				     url: '../../pages/animant/animantTwo?id='+e.currentTarget.id+'&src='+reciveanimantInfo_animantsrc1+'&title='+reciveanimantInfo_animant_title
				 });
			}
		}
	}
</script>
<style scoped>
	/*strat animant-autoside-box */
	 .animant-autoside-box{
		white-space: nowrap;
		overflow: hidden;
		/* width: 94%;
		margin: 3%; */
	 }
	 .animant-inside-box{
		    padding: 1%;
		    width: 98%;
		    height: 270rpx;
		    background-color: #FFFFFF;
		    /* border-radius: 12px; */
		    margin-bottom: 200rpx;
	}
	.animant-left-box{
		text-align: center;
		padding:5%;
		/* background-color: #E97352; */
	}
	.animant-left-box image{
		width: 100%;
		height: 300rpx;
		/* border-radius: 20rpx; */
		box-shadow: 0px 19px 25px rgba(255,255,255,0.35);
	}
	.animant-right-box{
		/* width:100%;
		height: 160rpx; */
		position: relative;
		bottom: 70rpx;
		left: 46rpx;
	}
	.animant-right-box .animant-right-r{
		/* float: left;
		margin-top: 16rpx;
		margin-left: 24rpx; */
	}
	.animant-right-r image{
		width: 40rpx;
		height: 20rpx;
		margin-bottom: -12rpx;
	}
	.animant-right-r .animant-r-up{
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
		width:100px;
		color:#fff;
		font-size: large;
		font-weight: bold;
		line-height: 1.2;
		margin-bottom: -4rpx;
	}
	.animant-right-r .animant-r-down{
		font-size: small;
		color: #fff;
	}
	.animant-right-box .animant-right-l{
		/* float: right; */
		text-align: right;
		width:60rpx;
		height:60rpx;
		padding: 2rpx;
		/* margin-top: 56rpx;
		margin-right:24rpx; */
		position: absolute;
		top: -60rpx;
		right: 108rpx;
	}
	.animant-right-l image{
		width: 40rpx;
		height: 40rpx;
		padding: 10rpx 4rpx 0rpx 0rpx;
	}
	 /*end animant-autoside-box */
</style>		