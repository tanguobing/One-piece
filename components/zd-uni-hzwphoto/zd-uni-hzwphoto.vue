<template name="zdUniPhoto">
	<view class="photo-autoside-box">
		<view class="photo-inside-box" v-for="(item,index) in recivephotoInfo" :id="item.id" :key="index" @click="navigators">
			<view class="photo-left-box">
				<image :src="item.photosrc1" mode=""></image>
			</view>
			<view class="photo-right-box">
				<view class="photo-right-r">
					<view class="photo-r-up">{{item.photo_title}}</view>
					<view class="photo-r-down">{{item.photo_content}}</view>
				</view>
				<view class="photo-right-l button_circle">
					<image :src="item.photosrc2" mode=""></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		name:"zdUniPhoto",
		props:["recivephotoInfo"],
		data() {
			return{
			}
		},
		methods:{
			navigators(e){
				let currentTargetid = Number(e.currentTarget.id);
				let recivephotoInfo_id,recivephotoInfo_photosrc1,recivephotoInfo_photo_title;
				console.log(typeof currentTargetid);
				for(let i = 0; i < this.recivephotoInfo.length;i++){
					if(currentTargetid === this.recivephotoInfo[i].id){
						recivephotoInfo_id = this.recivephotoInfo[i].id;
						recivephotoInfo_photosrc1 = this.recivephotoInfo[i].photosrc1;
						recivephotoInfo_photo_title = String(this.recivephotoInfo[i].photo_title);
					}
				}
				 uni.navigateTo({
				     url: '../../pages/hzwphoto/hzwphotoTwo?id='+e.currentTarget.id+'&src='+recivephotoInfo_photosrc1+'&title='+recivephotoInfo_photo_title
				 });
			}
		}
	}
</script>
<style scoped>
	/*strat photo-autoside-box */
	 .photo-autoside-box{
		white-space: nowrap;
		overflow: hidden;
		width: 94%;
		margin: 3%;
	 }
	 .photo-inside-box{
		    float: left;
		    padding: 2%;
		    width: 44%;
		    height: 400rpx;
		    background-color: #FFFFFF;
		    border-radius: 12px;
		    margin-bottom: 5px;
		    margin: 1%;
	}
	.photo-left-box{
		text-align: center;
		background-color: #E97352;
	}
	.photo-left-box image{
		width: 100%;
		height: 260rpx;
		border-radius: 20rpx;
	}
	.photo-right-box{
		width:100%;
		height: 160rpx;
	}
	.photo-right-box .photo-right-r{
		float: left;
		margin-top: 36rpx;
		margin-left: 24rpx;
	}
	.photo-right-r .photo-r-up{
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
		width:100px;
		color:#000000;
		font-size: unset;
		line-height: 1.2;
	}
	.photo-right-r .photo-r-down{
		font-size: small;
		color: rgba(0,0,0,0.35);
	}
	.photo-right-box .photo-right-l{
		float: right;
		text-align: right;
		width:40rpx;
		height:40rpx;
		padding: 2rpx;
		margin-top: 56rpx;
		margin-right:24rpx;
	}
	.photo-right-l image{
		width:24rpx;
		height:24rpx;
		padding:5rpx;
	}
	 /*end photo-autoside-box */
</style>		