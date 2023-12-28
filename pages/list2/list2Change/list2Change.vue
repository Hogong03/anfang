<template>
	<view id="root">
		<view class="list2Monitoring">扶梯监控平台</view>
		<view class="list2LocationAndTime">
			<view class="list2Loction" @click="showLocation()">地点:{{locationList[i].location}}</view>
			<view class="list2Time">{{timeNow}}</view>
		</view>
		<view class="list2Function1">
			<video muted="true" @timeupdate="onViedoTimeUpdate()" autoplay="true" loop="true"
				:src=monitorings[1]></video>
		</view>
		<view class="list2Function2">
			<ul v-for="item in dataMonitorings" :key="item.id">
				<li>{{item.name}}{{item.value}}</li>
			</ul>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				i: 1,
				locationList: [{
					location: "沁园"
				}, {
					location: "润园"
				}],
				timeNow: "",
				timeGet: true,
				monitorings: ["../../../static/video/escalatorMonitoring.mp4", ""],
				IntervalOen: true,
				change: true,
				timeID: "",
				timeID2: "",
				dataMonitorings: [{
					id: 1,
					name: "人数:",
					value: "100人"
				}, {
					id: 2,
					name: "载重:",
					value: "5600KG"
				}, {
					id: 3,
					name: "扶梯带速度:",
					value: "0.72m/s"
				}, {
					id: 4,
					name: "危险行为:",
					value: "无"
				}, {
					id: 5,
					name: "电机温度:",
					value: "50°C"
				}, {
					id: 6,
					name: "停止扶梯",
				}],
				dataMonitorings2: [{
					id: 1,
					name: "人数:",
					value: "120人"
				}, {
					id: 2,
					name: "载重:",
					value: "7600KG"
				}, {
					id: 3,
					name: "扶梯带速度:",
					value: "0.87m/s"
				}, {
					id: 4,
					name: "危险行为:",
					value: "无"
				}, {
					id: 5,
					name: "电机温度:",
					value: "56°C"
				}, {
					id: 6,
					name: "停止扶梯",
				}],
				dataMonitorings3: [{
					id: 1,
					name: "人数:",
					value: "80人"
				}, {
					id: 2,
					name: "载重:",
					value: "3600KG"
				}, {
					id: 3,
					name: "扶梯带速度:",
					value: "0.78m/s"
				}, {
					id: 4,
					name: "危险行为:",
					value: "无"
				}, {
					id: 5,
					name: "电机温度:",
					value: "45°C"
				}, {
					id: 6,
					name: "停止扶梯",
				}],
			}
		},
		methods: {
			onViedoTimeUpdate() {},
			showLocation() {
				const arr = new Array;
				const that = this
				for (let i = 0; i < this.locationList.length; i++) {
					arr[i] = this.locationList[i].location
				}
				uni.showActionSheet({
					title: "请选择地点",
					itemList: arr,
					success(e) {
						that.i = e.tapIndex
						that.monitoring = that.monitorings[e.tapIndex]
					}
				})
			}
		},
		onShow() {
			if (this.timeGet) {
				const that = this
				console.log("打开计时器");
				this.timeID = setInterval(function() {
					const now = new Date();
					var year = now.getFullYear();
					var month = (now.getMonth() + 1).toString().padStart(2, '0');
					var day = now.getDate().toString().padStart(2, '0');
					var hours = now.getHours().toString().padStart(2, '0');
					var minutes = now.getMinutes().toString().padStart(2, '0');
					var seconds = now.getSeconds().toString().padStart(2, '0');
					that.timeNow = year + '-' + month + '-' + day + ' ' + hours + ':' + minutes + ':' + seconds;
				}, 100)
				this.timeGet = !this.timeGet
				if (this.IntervalOen) {
					this.timeID2 = setInterval(() => {
						if (this.change) {
							this.dataMonitorings = this.dataMonitorings2
							this.change = !this.change
						} else {
							this.dataMonitorings = this.dataMonitorings3
							this.change = !this.change
						}
					}, 1000)
					this.IntervalOen = !this.IntervalOen
				}
			}
		},
		onHide() {
			if (!this.timeGet) {
				clearInterval(this.timeID)
				console.log("关闭计时器");
			}
			if (!this.IntervalOen) {
				clearInterval(this.timeID2)
			}
		},
		onLoad() {
			console.log("页面加载完成");
			const now = new Date();
			var year = now.getFullYear();
			var month = (now.getMonth() + 1).toString().padStart(2, '0');
			var day = now.getDate().toString().padStart(2, '0');
			var hours = now.getHours().toString().padStart(2, '0');
			var minutes = now.getMinutes().toString().padStart(2, '0');
			var seconds = now.getSeconds().toString().padStart(2, '0');
			this.timeNow = year + '-' + month + '-' + day + ' ' + hours + ':' + minutes + ':' + seconds;
		},
		onPullDownRefresh() {
			if (this.timeGet) {
				const that = this
				console.log("打开计时器");
				this.timeID = setInterval(function() {
					const now = new Date();
					var year = now.getFullYear();
					var month = (now.getMonth() + 1).toString().padStart(2, '0');
					var day = now.getDate().toString().padStart(2, '0');
					var hours = now.getHours().toString().padStart(2, '0');
					var minutes = now.getMinutes().toString().padStart(2, '0');
					var seconds = now.getSeconds().toString().padStart(2, '0');
					that.timeNow = year + '-' + month + '-' + day + ' ' + hours + ':' + minutes + ':' + seconds;
				}, 100)
				this.timeGet = !this.timeGet
				if (this.IntervalOen) {
					this.timeID2 = setInterval(() => {
						if (this.change) {
							this.dataMonitorings = this.dataMonitorings2
							this.change = !this.change
						} else {
							this.dataMonitorings = this.dataMonitorings3
							this.change = !this.change
						}
					}, 1000)
					this.IntervalOen = !this.IntervalOen
				}
			}
			console.log('refresh');
			setTimeout(function() {
				uni.stopPullDownRefresh();
				uni.showToast({
					title: "刷新成功",
					icon: "success"
				})
			}, 1000);
		}
	}
</script>

<style lang="scss" scoped>
	#root {
		height: 100vh;
		width: 100vw;
		background-image: linear-gradient(to bottom, #242c2f, #616e72);
		// background-image: linear-gradient(to bottom, #141E30, #243B55);
		overflow: hidden;
		color: #c0c4cc;

		.list2Monitoring {
			text-align: center;
			height: 7vh;
			font-size: 36rpx;
			line-height: 11vh;
			background-image: linear-gradient(to bottom, #141E30, #243B55);
			opacity: 0.6;
		}

		.list2LocationAndTime {
			margin-top: 2vh;
			height: 4vh;
			margin-left: 2vw;

			.list2Loction {
				float: left;
				height: 4vh;
				line-height: 4vh;
				width: 24vw;
				text-align: center;
				font-size: 32rpx;
			}

			.list2Time {
				float: left;
				height: 4vh;
				line-height: 4vh;
				width: 48vw;
				font-size: 20rpx;
			}

		}

		.list2Function1 {
			margin-top: 2vh;
			height: 42vh;
			width: 100vw;

			video {
				height: 100%;
				width: 100%;
			}
		}

		.list2Function2 {
			height: 28vh;
			border: black solid 1rpx;
			margin-top: 2vh;
			width: 96vw;
			margin: 2vh auto;
			border-radius: 24rpx;
			box-shadow: 0rpx 0rpx 4rpx #d5ffed;

			ul {
				li {
					display: block;
					width: 42vw;
					line-height: 8vh;
					text-align: center;
					height: 8vh;
					float: left;
					border: gray solid 1rpx;
					margin: 1vh 0vw 0vh 4vw;
					border-radius: 12rpx;
					box-shadow: 0rpx 0rpx 2rpx #f3f4f6;
					background-image: linear-gradient(to bottom, #141E30, #243B55);
				}
			}
		}
	}
</style>