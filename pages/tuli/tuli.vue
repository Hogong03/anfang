<template>
	<view class="charts-box">
		<qiun-data-charts type="gauge" :opts="opts" :chartData="chartData" />
	</view>
</template>

<script>
	export default {
		data() {
			return {
				chartData: {},
				//您可以通过修改 config-ucharts.js 文件中下标为 ['gauge'] 的节点来配置全局默认参数，如都是默认参数，此处可以不传 opts 。实际应用过程中 opts 只需传入与全局默认参数中不一致的【某一个属性】即可实现同类型的图表显示不同的样式，达到页面简洁的需求。
				opts: {
					animation:false,
					duration: 1200,
					background: 'rgba(40, 44, 53)',
					color: ["#1890FF", "#91CB74", "#FAC858", "#EE6666", "#73C0DE", "#3CA272", "#FC8452", "#9A60B4",
						"#ea7ccc"
					],
					padding: [100,105,200,300], //画布填充边距，顺序为上右下左，例如[10,15,25,15]
					title: {
						name: "温度/°C",
						fontSize: 25,
						color: "#2fc25b",
						offsetY: 50
					},
					subtitle: {
						name: "实时温度",
						fontSize: 15,
						color: "#666666",
						offsetY: -50
					},
					extra: {
						gauge: {
							type: "default",
							width: 20,
							labelColor: "#666666",
							startAngle: 0.7,
							endAngle: 0.3,
							startNumber: 30,
							endNumber: 60,
							labelFormat: "",
							splitLine: {
								fixRadius: 0,
								splitNumber: 10,
								width: 30,
								color: "#FFFFFF",
								childNumber: 5,
								childWidth: 12
							},
							pointer: {
								width: 20,
								color: "auto"
							}
						}
					}
				}
			};
		},
		onReady() {
			this.getServerData();
		},
		methods: {
			getServerData() {
				//模拟从服务器获取数据时的延时
				setTimeout(() => {
					//模拟服务器返回数据，如果数据格式和标准格式不同，需自行按下面的格式拼接
					let res = {
						animation:false,
						categories: [{
							"value": 0.2,
							"color": "#1890ff"
						}, {
							"value": 0.8,
							"color": "#2fc25b"
						}, {
							"value": 1,
							"color": "#f04864"
						}],
						series: [{
							name: "完成率",
							data: 0.8
						}]
					};
					this.chartData = JSON.parse(JSON.stringify(res));
				}, 500);
			},
		}
	};
</script>

<style scoped>
	/* 请根据实际需求修改父元素尺寸，组件自动识别宽高 */
	.charts-box {
		width: 100%;
		height: 300px;
	}
</style>