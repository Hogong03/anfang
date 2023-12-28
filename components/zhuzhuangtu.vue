<template>
	<view class="charts-box">
		<qiun-data-charts type="arcbar" :opts="opts" :chartData="chartData" />
	</view>
</template>

<script>
	export default {
		data() {
			return {
				chartData: {
					series: [{
						name: "正确率",
						color: "#2fc25b",
						data: 0.3
					}]
				},
				//您可以通过修改 config-ucharts.js 文件中下标为 ['arcbar'] 的节点来配置全局默认参数，如都是默认参数，此处可以不传 opts 。实际应用过程中 opts 只需传入与全局默认参数中不一致的【某一个属性】即可实现同类型的图表显示不同的样式，达到页面简洁的需求。
				opts: {
					color: ["#1890FF", "#91CB74", "#FAC858", "#EE6666", "#73C0DE", "#3CA272", "#FC8452", "#9A60B4",
						"#ea7ccc"
					],
					padding: undefined,
					title: {
						name: "12人",
						fontSize: 35,
						color: "#2fc25b"
					},
					subtitle: {
						name: "人数",
						fontSize: 25,
						color: "#666666"
					},
					extra: {
						arcbar: {
							type: "default",
							width: 12,
							backgroundColor: "#E9E9E9",
							startAngle: 0.75,
							endAngle: 0.25,
							gap: 2,
							linearType: "custom"
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
						series: [{
							name: "正确率",
							color: "#2fc25b",
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
		height: 240px;
	}
</style>