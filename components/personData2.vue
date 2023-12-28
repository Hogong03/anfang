<template>
	<view class="charts-box">
		<qiun-data-charts type="line" :opts="opts" :chartData="chartData" />
	</view>
</template>

<script>
	export default {
		data() {
			return {
				chartData: {
					categories: ["10:00", "12:00", "14:00", "16:00", "18:00", "20:00"],
					series: [{
							name: "总人数",
							data: [214, 190, 143, 202, 76, 26]
						}, {
							name: "成年人",
							data: [120, 88, 74, 82, 40, 12]
						},
						{
							name: "老人",
							data: [30, 22, 24, 70, 14, 8]
						},
						{
							name: "小孩",
							data: [64, 80, 45, 50, 22, 6]
						},
						{
							name: "总人数",
							data: [214, 190, 143, 202, 76, 26]
						}
					]
				},
				//您可以通过修改 config-ucharts.js 文件中下标为 ['line'] 的节点来配置全局默认参数，如都是默认参数，此处可以不传 opts 。实际应用过程中 opts 只需传入与全局默认参数中不一致的【某一个属性】即可实现同类型的图表显示不同的样式，达到页面简洁的需求。
				opts: {
					animation: "false",
					fontColor: "#252525",
					dataLabel: false,
					// enableScroll: true,
					color: ["#91CB74", "#1890FF", "#FAC858", "#EE6666", ],
					padding: [15, 10, 5, 5],
					enableScroll: false,
					legend: {
						position: "top",
						float: "left",
					},
					xAxis: {
						// disableGrid: true,
						scrollShow: true,
						itemCount: 2,
						fontColor: "#252525",
					},
					yAxis: {
						gridType: "dash",
						dashLength: 2
					},
					extra: {
						line: {
							type: "curve",
							width: 1,
							activeType: "none",
							onShadow: true,
						}
					},
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
						categories: ["2018", "2019", "2020", "2021", "2022", "2023"],
						series: [{
								name: "成交量A",
								data: [35, 8, 25, 37, 4, 20]
							},
							{
								name: "成交量B",
								data: [70, 40, 65, 100, 44, 68]
							},
							{
								name: "成交量C",
								data: [100, 80, 95, 150, 112, 132]
							}
						]
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
		height: 100%;
	}
</style>