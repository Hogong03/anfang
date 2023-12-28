<template>
	<view id="list1Function">
		<view class="list1Title">扶梯数据可视化平台</view>
		<view class="list1LocationAndTime">
			<view class="list1Loction" @click="showLocation()">地点:{{locationList[i].location}}</view>
			<view class="list1Time">{{timeNow}}</view>
		</view>
		<view class="list1FunctionDataSummary">
			<view class="dataUl">
				<ul v-for="item in dataSummary" :key="item.id">
					<li>
						<span>{{item.title}}</span>
						<view class="dataSummaryValue">{{item.value}}</view>
					</li>
				</ul>
			</view>
		</view>
		<view class="DataVisualization1">
			<view class="DataVisualization1Detail">人流量数据:</view>
			<view class="DetailForm">
				<personData></personData>
			</view>
			<view class="behaviorMonitoring">行为总结:</view>
			<view class="behaviors">
				<ul v-for="item in behaviors" :key="item.id">
					<li><span>{{item.name}}</span>{{item.value}}</li>
				</ul>
			</view>
		</view>
		<view class="DV2">扶梯数据流:</view>
		<view class="DataVisualization2">
			<view class="escalatorData">
				<ul class="DVUl" v-for="item in escalatorData" :key="item.id">
					<li @click="escalatorDataChoose(item.id)">
						<span>{{item.title}}</span>
						<view class="detailData">{{item.value}}</view>
					</li>
				</ul>
			</view>
		</view>
		<view class="dataChoose">
			<personData2 v-if="this.dataChoose === 2" ref="personData2"></personData2>
			<personData3 v-if="this.dataChoose === 3"></personData3>
			<personData4 v-if="this.dataChoose === 4" v-model="timeGet"></personData4>
		</view>
	</view>
</template>

<script>
	import personData from "../../../components/personData.vue";
	import personData2 from "../../../components/personData2.vue";
	import personData3 from "../../../components/personData3.vue";
	import personData4 from "../../../components/personData4.vue";
	export default {
		data() {
			return {
				timeNow: "",
				timeGet: true,
				timeID: "",
				locationList: [{
					location: "沁园"
				}, {
					location: "润园"
				}],
				i: 1,
				dataSummary: [{
						id: 1,
						title: "总人数",
						value: 4800 + "人",
					},
					{
						id: 2,
						title: "上行人数",
						value: 2200 + "人",
					},
					{
						id: 3,
						title: "下行人数",
						value: 2600 + "人",
					},
					{
						id: 4,
						title: "平均人流量",
						value: 400 + "人/H",
					},
				],
				behaviors: [{
					id: 1,
					name: "警告行为:",
					value: 20
				}, {
					id: 2,
					name: "危险行为:",
					value: 6
				}, {
					id: 3,
					name: "极其危险行为:",
					value: 0
				}, ],
				escalatorData: [{
					id: 1,
					title: "人流量",
					value: 52 + "人"
				}, {
					id: 2,
					title: "发动机温度",
					value: 56 + "°C"
				}, {
					id: 3,
					title: "行为总结",
					value: 12 + "警报行为"
				}, ],
				dataChoose: 2,
			}
		},
		mounted() {
			this.$refs.personData2.$on('ISGS', this.Hello)
		},
		methods: {
			Hello() {
				console.log(Hello);
			},
			escalatorDataChoose(e) {
				this.dataChoose = e + 1;
			},
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
				}, 1000)
				this.timeGet = !this.timeGet
			}
		},
		onHide() {
			if (!this.timeGet) {
				clearInterval(this.timeID)
				console.log("关闭计时器");
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
		components: {
			personData,
			personData2,
			personData3,
			personData4,
		}
	}
</script>

<style lang="scss" scoped>
	#list1Function {
		height: 100vh;
		width: 100vw;
		background-image: linear-gradient(to bottom, #242c2f, #616e72);
		color: #c0c4cc;
		overflow: scroll;
		// background-image: linear-gradient(to bottom, #141E30, #243B55);
		background-size: cover;
		opacity: 0.98;

		.list1Title {
			height: 7vh;
			width: 100vw;
			text-align: center;
			line-height: 11vh;
			font-size: 36rpx;
			position: fixed;
			opacity: 0.6;
			background-image: linear-gradient(to bottom, #141E30, #243B55);
			border-bottom-left-radius: 24rpx;
			border-bottom-right-radius: 24rpx;
		}

		.list1LocationAndTime {
			margin-top: 8vh;
			height: 4vh;

			.list1Loction {
				float: left;
				height: 4vh;
				line-height: 4vh;
				width: 24vw;
				text-align: center;
				font-size: 32rpx;
			}

			.list1Time {
				float: left;
				height: 4vh;
				line-height: 4vh;
				width: 36vw;
				font-size: 20rpx;
			}

		}


		.list1FunctionDataSummary {
			height: 14vh;
			border-radius: 24rpx;
			width: 96vw;
			margin: 2vh auto;
			border: #242c2f solid 1rpx;
			background-image: linear-gradient(to bottom, #252525, #242c2f);

			.dataUl {
				ul {
					li {
						float: left;
						width: 20vw;
						height: 100%;

						span {
							margin-top: 4vh;
							font-size: 20rpx;
							color: #616e72;
							height: 4vh;
							width: 20vw;
							display: block;
							text-align: center;
						}

						.dataSummaryValue {
							height: 4vh;
							text-align: center;
							color: #f3f4f6;
							font-size: 28rpx;
						}
					}
				}
			}
		}

		.DataVisualization1 {
			height: 28vh;
			width: 96vw;
			margin: 2vh auto;
			border: gray solid 1rpx;
			position: relative;
			background-color: #252525;
			border-radius: 24rpx;
			background-image: linear-gradient(to right, #252525, #414144);

			.DataVisualization1Detail {
				height: 4vh;
				line-height: 4vh;
				text-indent: 1em;
			}

			.DetailForm {
				height: 24vh;
				width: 56vw;
				// border: red solid 1rpx;
				font-size: 16rpx;
				overflow: scroll;
			}

			.behaviorMonitoring {
				position: absolute;
				height: 4vh;
				line-height: 4vh;
				left: 56vw;
				top: 0;
			}

			.behaviors {
				position: absolute;
				left: 60vw;
				top: 6vh;

				ul {
					li {
						height: 4vh;
						line-height: 4vh;

						span {
							display: block;
							width: 24vw;
							float: left;
						}
					}
				}
			}
		}

		.DV2 {
			text-indent: 1em;
			// color: #aeaeae;
			color: #f3f4f6;
			font-weight: 700;
			font-size: 32rpx;
		}

		.DataVisualization2 {
			height: 12vh;
			width: 96vw;
			margin: 2vh auto;
			border: gray solid 1rpx;
			overflow: scroll;
			border-radius: 24rpx;

			.escalatorData {
				ul {
					li {
						height: 8vh;
						width: 24vw;
						float: left;
						margin-left: 6vw;
						margin-top: 2vh;
						background-color: #242425;
						border-radius: 24rpx;

						span {
							width: 100%;
							display: block;
							height: 4vh;
							line-height: 4vh;
							text-align: center;
						}

						.detailData {
							height: 4vh;
							line-height: 4vh;
							text-align: center;
						}
					}
				}
			}
		}

		.dataChoose {
			height: 32vh;
			width: 100vw;
			margin: 2vh auto;
			color: red;
		}
	}
</style>