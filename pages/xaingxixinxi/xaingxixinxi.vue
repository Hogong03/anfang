<template>
	<view class="mainbody">
		<view class="mar"></view>
		<view class="juti">具体数据</view>
		<view class="xiangqing">
			<view class="mingcheng">
				<ul v-for="mc in mingcheng" :key="mc.id">
					<li>{{mc.name}}</li>
				</ul>
			</view>
			<view class="shuxing">
				<ul v-for="mcc in mingcheng" :key="mcc.id">
					<li @click="tofutizhengshu(mcc.isActive)" :class="{ zhengshu: mcc.isActive }">{{mcc.value}}</li>
				</ul>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				weizhi: 'NIT',
				bianhao: 'abc',
				mingcheng: [{
						name: '名称',
						value: '智能扶梯',
						id: 1,
						isActive: false
					},
					{
						name: '位置',
						value: 'NIT',
						id: 2,
						isActive: false
					},
					{
						name: '扶梯编号',
						value: 'abcd',
						id: 3,
						isActive: false
					},
					{
						name: '长宽高',
						value: '12m,2m,8m',
						id: 4,
						isActive: false
					},
					{
						name: '倾斜角',
						value: '30°',
						id: 5,
						isActive: false
					},
					{
						name: '额定重量（人数）',
						value: '30吨（50人）',
						id: 6,
						isActive: false
					},
					{
						name: '功率',
						value: '30kw',
						id: 7,
						isActive: false
					},
					{
						name: '证书',
						value: '扶梯证书',
						id: 8,
						isActive: true
					}
				]
			}
		},
		onLoad() {},
		methods: {
			tofutizhengshu(index) {
				if (index) {
					uni.showLoading({
						title:"加载中"
					})
					setTimeout(function() {
						uni.navigateTo({
							url: '/pages/futizhengshu/futizhengshu',
							success: res => {},
							fail: () => {},
							complete: () => {
								uni.hideLoading()
							}
						});
					}, 200);
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	.mainbody {
		font-size: 28rpx;
		height: 100vh;
		width: 100vw;
		background-color: gray;

		.zhengshu {
			color: blue;
			text-decoration: underline;
			border: 1rpx black solid;
			text-indent: 1em;
		}

		.juti {
			height: 48rpx;
			text-align: center;
			border: 1rpx black solid;
			width: 80%;
			margin: auto;
		}

		.mar {
			height: 64rpx;
		}

		.xiangqing {
			width: 80%;
			margin: auto;

			.mingcheng {
				float: left;

				ul {
					li {
						display: block;
						border: 1rpx black solid;
						margin: 0rpx;
						text-indent: 1em;
					}
				}
			}

			.shuxing {
				ul {
					li {
						border: 1rpx black solid;
						display: block;
						text-align: center;
					}
				}
			}
		}
	}
</style>