<template>
	<view class="setting">
		<view class="mar"></view>
		<view class="image">
			<image src="../../../static/info.png" mode=""></image>
		</view>
		<view class="versionInfo">{{versionInfo}}</view>
		<view class="versionInfoDetail">
			{{details}}
		</view>
		<view class="updataDetails">
			<view class="title">更新内容：</view>
			<ul v-for="item in updateDetails" :key="item.id">
				<li>{{item.id}}.{{item.detail}}</li>
			</ul>
		</view>
		<view class="uButton">
			<u-button @click="updateChecking()" size="mdeium" :disabled=disabled :loading=showLoading
				type="primary">检查版本更新</u-button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				versionInfo: "智能安防系统2.01",
				details: "扶梯智能安防系统是一款基于JS,Java技术为基础的为用户提供扶梯监控，管理，数据可视化的APP。以为您提供智能化的扶梯管理",
				showLoading: false,
				disabled: false,
				updateDetails: [{
					id: 1,
					detail: "页面优化",
				}, {
					id: 2,
					detail: "功能增加",
				}, {
					id: 3,
					detail: "操作优化",
				}, {
					id: 4,
					detail: "Bug修复",
				}, ]
			}
		},
		methods: {
			updateChecking() {
				this.showLoading = true
				this.disabled = true
				setTimeout(() => {
					uni.showToast({
						title: '当前已经是最新版本',
						icon: "none",
						success: () => {
							this.showLoading = false
							this.disabled = false
						}
					});
				}, 800);
			}
		},
		onLoad() {}
	}
</script>

<style lang="scss">
	.setting {
		overflow: hidden;
		background-color: #dcdfe6;
		height: 100vh;
		width: 100vw;

		.mar {
			height: 3vh;
		}

		.image {
			height: 8vh;
			width: 20vw;
			margin: 24rpx auto;

			image {
				height: 100%;
				width: 100%;
			}
		}

		.uButton {
			width: 64vw;
			margin: 18vh auto;
		}

		.versionInfo {
			width: 56vw;
			text-align: center;
			margin: 10rpx auto;
			font-size: 36rpx;
			font-weight: 700;
		}

		.versionInfoDetail {
			width: 78vw;
			margin: 32rpx auto;
			text-align: center;
			font-weight: 400;
			font-size: 28rpx;
		}

		.updataDetails {
			height: 24vh;
			width: 88vw;
			margin: 12rpx auto;

			.title {
				font-weight: 600;
				font-size: 28rpx;
			}

			ul {
				li {
					font-size: 24rpx;
					font-weight: 300;
					width: 100vw;
					height: 2.8vh;
					line-height: 2.8vh;
					text-indent: 1em;
				}
			}
		}
	}
</style>