<script>
export default {
	onLaunch: function() {
		console.log('App Launch');
		// #ifdef APP-PLUS
		// 检测升级
		uni.request({
		    url: 'https://uniapp.dcloud.io/update', //检查更新的服务器地址
		    data: {
		        appid: plus.runtime.appid,
		        version: plus.runtime.version,
		        imei: plus.device.imei
		    },
		    success: (res) => {
				console.log(res)
				console.log(plus.os)
				console.log(res.data)
		        if (res.statusCode == 200 && res.data.isUpdate) {
		            let openUrl = plus.os.name === 'iOS' ? res.data.iOS : res.data.Android;
		            // 提醒用户更新
		            uni.showModal({
		                title: '更新提示',
		                content: res.data.note ? res.data.note : '是否选择更新',
		                success: (showResult) => {
		                    if (showResult.confirm) {
		                        plus.runtime.openURL(openUrl);
		                    }
		                }
		            })
		        }
		    }
		})
		// #endif
	},
	onShow: function() {
		console.log('App Show');
	},
	onHide: function() {
		console.log('App Hide');
	}
};
</script>

<style>
	/* 解决头条小程序组件内引入字体不生效的问题 */
	/* #ifndef APP-PLUS-NVUE */
	/*uni.css -通用组件、模板样式库*/
	@import './common/uni.css';
	html body{
		background-color: #E97352;	
	}
	/* circle */
	.button_circle{
		border-radius: 60rpx;
		background: rgba(158,49,62,0.45);
		box-shadow: 0px 10px 24px 1px rgba(158,49,62,0.27);
	}
	/* circle */ 
	/* #endif */
	
	/* #ifdef MP-360 */
	::-webkit-scrollbar {width: 4px; height: 4px; background-color: transparent;}
	::-webkit-scrollbar-track {background-color: transparent;}
	::-webkit-scrollbar-thumb {background-color: #ddd;}
	::-webkit-scrollbar-thumb:hover {background-color: #ccc;}
	::-webkit-scrollbar-thumb:active {background-color: #bbb;}
	::-webkit-scrollbar-corner {background: #ffffff;}
	/* #endif*/
</style>