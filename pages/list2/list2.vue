<template>
	<view class="mianList2">
		<view class="mar"></view>
		<view class="partion2">
			<view class="weixian" @click="locationChange()">地点:{{location}}</view>
			<view class="xingwei">行为判断:{{action[0]}}</view>
			<view class="shipinjiankong">
				<video muted="true" @timeupdate="onViedoTimeUpdate" autoplay="true" loop="true" :src=monitoring
					class="viedoList2"></video>
			</view>
		</view>
		<view class="partion3" v-if="this.yemiann === true">
			<zhuzhuangtu v-if="this.list2UCharts === 1"></zhuzhuangtu>
			<speed v-if="this.list2UCharts === 2"></speed>
			<view v-if="this.list2UCharts === 2" class="upDownSpeed">
				<view class="escalatorSpeed">{{upSpeed}}</view>
				<view class="escalatorSpeed down">{{downSpeed}}</view>
			</view>
			<shishiwendu v-if="this.list2UCharts === 3"></shishiwendu>
			<pinlv v-if="this.list2UCharts === 4"></pinlv>
		</view>
		<view class="dataList">
			<view class="shujuliebiao" v-for="item in uButton" :key="item.id">
				<u-button class="u-button" :type=item.type :color=item.color
					@click="uButtonClick(item.id)">{{item.detail}}{{item.value}}<br>{{item.subdetail}}{{item.subvalue}}
				</u-button>
			</view>
		</view>
	</view>
</template>

<script>
	import zhuzhuangtu from '../../components/zhuzhuangtu.vue';
	import shishiwendu from '../../components/shishiwendu.vue';
	import pinlv from '../../components/pinlv.vue';
	import speed from '../../components/speed.vue';
	export default {
		data() {
			return {
				action: ['正常', '肢体伸出区域外', '推车', '摔倒'],
				panduan: 1,
				yemiann: false,
				location: '润园',
				xiangqing: "扶梯数据",
				upSpeed: "上行速度" + 0.69 + "m/s",
				downSpeed: "下行速度" + 0.71 + "m/s",
				list2UCharts: 1,
				timerId: "",
				dataDemand: true,
				monitoring: "../../static/video/escalatorMonitoring.mp4",
				uButton: [{
					id: 1,
					detail: "上行人数:",
					type: "primary",
					value: "8人",
					subdetail: "下行人数",
					subvalue: '4人',
					color: "#7094b3"
				}, {
					id: 2,
					detail: "上行速度:",
					type: "primary",
					value: "0.69m/s",
					subdetail: "下行速度",
					subvalue: '0.71m/s',
					color: "#7094b3"
				}, {
					id: 3,
					detail: "扶梯温度:",
					type: "primary",
					value: "42°C",
					color: "#7094b3"
				}, {
					id: 4,
					detail: "扶梯频率:",
					type: "primary",
					value: "70HZ/s",
					color: "#7094b3"
				}, {
					id: 5,
					detail: "安全按钮",
					type: "error",
					value: '',
				}, {
					id: 6,
					detail: "扶手状态",
					type: "success",
					value: ":正常",
				}, ],
				locations: [{
					id: 1,
					location: "润园"
				}, {
					id: 2,
					location: "沁园"
				}]
			};
		},
		methods: {
			onViedoTimeUpdate(){},
			uButtonClick(e) {
				console.log(e);
			},
			locationChange() {
				var arr = [];
				for (let i = 0; i < this.locations.length; i++) {
					arr[i] = this.locations[i].location
				}
				const that = this
				uni.showActionSheet({
					itemList: arr,
					success(e) {
						that.location = arr[e.tapIndex]
					},
				})
			}
		},
		onShow() {
			// if (this.dataDemand) {
			// 	this.timerId = setInterval(() => {
			// 		console.log("数据请求中");
			// 	}, 500)
			// 	this.dataDemand = false
			// }
		},
		onHide() {
			clearInterval(this.timerId)
			console.log("数据停止请求");
			this.dataDemand = true
		},
		components: {
			zhuzhuangtu,
			shishiwendu,
			pinlv,
			speed,
		}
	}
</script>

<style lang="scss" scoped>
	.mianList2 {
		height: 100vh;
		width: 100vw;
		padding: 0rpx;
		margin: 0rpx;
		background-image: linear-gradient(to bottom, #242c2f, #616e72);

		.mar {
			height: 6vh;
			background-color: #242c2f;
		}

		.partion2 {
			height: 600rpx;

			.weixian {
				text-align: center;
				width: 36vw;
				background-color: #000000;
				color: #8A9BA8;
				height: 40rpx;
				line-height: 40rpx;
			}

			.xingwei {
				background-color: #E2E2E2;
				text-align: center;
				font-size: 48rpx;
				height: 60rpx;
				line-height: 60rpx;
				background-color: white;
			}

			.shipinjiankong {
				height: 560rpx;
				width: 750rpx;
				margin: 10rpx auto;

				.viedoList2 {
					height: 560rpx;
					width: 750rpx;
					margin: 0rpx auto;
				}
			}
		}

		.modeloption {
			margin: 24rpx auto;

			.submoption {
				width: 180rpx;
				font-size: 18rpx;
				margin: 6rpx auto;
				font-size: 26rpx;
			}
		}

		.partion3 {
			position: relative;
			height: 600rpx;

			.upDownSpeed {
				position: absolute;
				left: 1vw;
				top: 0vh;

				.escalatorSpeed {
					border: skyblue 1rpx solid;
					margin-top: 6rpx;
					font-size: 18rpx;
					height: 42rpx;
					width: 18vw;
					line-height: 42rpx;
				}

				.down {
					border: green solid 1rpx;
				}
			}

			.partion3-button {
				width: 12vw;
				font-size: 2vw;
				float: right;
				color: black
			}

			.shuju {
				width: 60vw;
				margin: 10rpx auto;

				.shujus {
					width: 24vw;
					float: left;
					margin-left: 4vw;
				}
			}
		}

		.dataList {
			// border: 1rpx red solid;
			height: 40vh;
			background-color: #273333;
			border-top: 64rpx gray solid;

			.shujuliebiao {
				width: 96vw;
				margin: 10rpx auto;

				.u-button {
					width: 42vw;
					height: 8vh;
					float: left;
					margin-left: 4vw;
					margin-top: 2vh;
				}
			}
		}

	}
</style>