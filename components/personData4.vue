<template>
	<view class="charts-box">
		<qiun-data-charts type="line" :opts="opts" :chartData="chartData" :ontouch="true" />
	</view>
</template>

<script>
	export default {
		data() {
			return {
				chartData: {
					categories: ["2018", "2019", "2020", "2021", "2022", "2023"],
					series: [{
							name: "警报行为",
							data: [10, 9, 8, 12, 7, 11]
						},
						{
							name: "危险行为",
							data: [2, 4, 1, 0, 3, 2]
						},
						{
							name: "总行为",
							data: [12, 13, 9, 12, 10, 13]
						}
					]
				},
				//您可以通过修改 config-ucharts.js 文件中下标为 ['line'] 的节点来配置全局默认参数，如都是默认参数，此处可以不传 opts 。实际应用过程中 opts 只需传入与全局默认参数中不一致的【某一个属性】即可实现同类型的图表显示不同的样式，达到页面简洁的需求。
				opts: {
					color: ["#FAC858", "#EE6666", "#91CB74", "#EE6666", "#73C0DE", "#3CA272", "#FC8452", "#9A60B4", ],
					padding: [0, 10, 0, 10],
					enableScroll: true,
					scrollBackgroundColor: "#252525",
					bacgroundColor: "#252525",
					fontColor: "#252525",
					legend: {
						fontSize: "8",
						position: "top",
						float: "left",
					},
					xAxis: {
						disableGrid: true,
						scrollShow: true,
						itemCount: 4,
						scrollColor: "#252525",
						scrollBackgroundColor: "#f3f4f6",
						gridColor: "#252525",
						fontColor: "#252525"
					},
					yAxis: {
						gridType: "dash",
						dashLength: 2,
						gridColor: "#252525"
					},
					extra: {
						line: {
							type: "straight",
							width: 2,
							activeType: "hollow"
						}
					}
				}
			};
		},
		onReady() {
			console.log(1);
			this.getServerData();
			console.log(2);
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
		},
		props: ['timeGet'],
		onLoad() {
			console.log("图标4正在启动");
			console.log(this.timeGet);
			console.log("图标4启动完成");
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