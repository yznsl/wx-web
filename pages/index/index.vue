<template>
	<view class="content">
		<view class="text-area">
			<text class="title">{{title}}</text>
		</view>
		<button @click="scanCode">扫一下呗</button>
	</view>
</template>

<script>
	import wx from 'weixin-js-sdk'
	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
		onLoad(e) {
			console.log(e)
		},
		methods: {
			getInfo(){
				uni.request({
					url: 'http://xx.haileer.top:8901/wx_jsapi_ticket', // 此处找后端要接口 微信不能使用端口访问端口改为 wx
					method: 'GET',
					success: (response) => {
						const res = response.data;
						if (res.code == "1") {
							console.log("res", res);
							
						} else {
							console.log('获取配置信息返回为空');
						}
					},
					fail: error => {
						console.log(error, '请求获取微信配置失败 请求方法：http://xx.haileer.top:8901/wx_jsapi_ticket');
					}
				});
			},
			scanCode(){
				console.log("hello")
				// var wx = require('weixin-js-sdk');
				wx.scanQRCode({
					needResult: 1, // 默认为0，扫描结果由微信处理，1则直接返回扫描结果，
					scanType: ["qrCode","barCode"], // 可以指定扫二维码还是一维码，默认二者都有
					success: function (res) {
						var result = res.resultStr; // 当needResult 为 1 时，扫码返回的结果
						console.log(result)
					},
					fail(res){
						console.log("fail： " )
						console.log(res)
					}
				})
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
