<template>
	<view>
		<view @click="startScan" class="scan-button">
			点击扫码连接WiFi
		</view>
	</view>
</template>

<script>
	export default {
		name: "WiFiConnector",
		data() {
			return {
				wifiInfo: null, // 存储WiFi信息
				connected: false // 标识是否已连接WiFi
			};
		},
		 onLoad(options) {
		    console.log('页面加载时的路径和参数:', options);
		  },
		methods: {
			// 开始扫码
			startScan() {
				uni.scanCode({
					success: (res) => {
						console.log('扫码结果:', res);
						const wifiInfo = this.parseWiFiInfo(res.result);
						console.log("wifiinfo是", wifiInfo);
						if (wifiInfo) {
							
							this.connectToWiFi(wifiInfo.ssid, wifiInfo.password);

						} else {
							uni.showToast({
								title: '无效的WiFi信息',
								icon: 'none'
							});
						}
					},
					fail: (err) => {
						console.error('扫码失败:', err);
						uni.showToast({
							title: '扫码失败',
							icon: 'none'
						});
					}
				});
			},
			// 解析WiFi信息
			parseWiFiInfo(qrData) {
			    console.log('解析二维码内容:', qrData);
			    // 正则表达式只提取SSID和密码
			   const match = qrData.match(/wifi名称:(.*?)密码:(.*)/);
			    console.log('正则匹配结果:', match);
			    if (match) {
			        return {
			            ssid: match[1],     // WiFi 名称
			            password: match[2]  // WiFi 密码
			        };
			    }
			    return null;
			},


			// 连接WiFi
			connectToWiFi(ssid, password) {
				uni.startWifi({
					success: () => {
						uni.connectWifi({
							SSID: ssid,
							password: password,
							success: () => {
								this.connected = true;
								this.wifiInfo = {
									ssid,
									password
								};
								uni.showToast({
									title: 'WiFi连接成功',
									icon: 'success'
								});
							},
							fail: (err) => {
								console.error('连接WiFi失败:', err);
								uni.showToast({
									title: 'WiFi连接失败',
									icon: 'none'
								});
							}
						});
					},
					fail: (err) => {
						console.error('启动WiFi模块失败:', err);
						uni.showToast({
							title: '启动WiFi模块失败',
							icon: 'none'
						});
					}
				});
			}
		}
	};
</script>

<style lang="scss">
	.scan-button {
		width: 200px;
		height: 50px;
		background-color: #007aff;
		color: #fff;
		text-align: center;
		line-height: 50px;
		border-radius: 5px;
		margin: 20px auto;
		font-size: 16px;
	}
</style>