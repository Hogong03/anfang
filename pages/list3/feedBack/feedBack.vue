<template>
	<view id="root">
		<view class="mar" style="height: 3vh;"></view>
		<view class="title">反馈内容：</view>
		<view class="mainbody">
			<ul>
				<li v-for="item in feedBacks" :key="item.id">
					<view class="feedbackTitle">{{item.title}}</view>
					<view class="feedbackText">
						<input type="text" :placeholder="item.content" v-model="item.value" />
					</view>
					<view class="feedbackButton"><u-button type="primary" plain shape="circle"
							@click="submit(item.value)" size="mini">提交</u-button>
					</view>
				</li>
			</ul>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				feedBacks: [{
					id: 1,
					title: "Bug",
					content: "期待您的反馈",
					value: "",
				}, {
					id: 2,
					title: "UL设计",
					content: "期待您的反馈",
					value: "",
				}, {
					id: 3,
					title: "操作反馈",
					content: "期待您的反馈",
					value: "",
				}, {
					id: 4,
					title: "其他",
					content: "期待您的反馈",
					value: "",
				}, ]
			}
		},
		methods: {
			submit(e) {
				if (e === "") {
					uni.showToast({
						title: "请输入内容",
						icon: "error",
						success() {
							console.log("反馈失败");
						}
					})
				} else {
					uni.showToast({
						title: "提交成功",
						icon: "success",
						success() {
							console.log("提交成功");
						}
					})
				}
			},
			toValue(e) {
				return this.feedBacks[e - 1].value
			}
		}
	}
</script>

<style lang="scss">
	#root {
		height: 100vh;
		width: 100vw;
		background-color: #dcdfe6;

		.title {
			width: 100vw;
			text-align: center;
			margin-bottom: 6vh;
		}

		.mainbody {
			ul {
				li {
					position: relative;
					height: 10vh;
					border: 1rpx red solid;
					margin: 24rpx auto;
					border-radius: 18rpx;
					overflow: hidden;

					.feedbackTitle {
						background-color: #c4c6c9;
						position: absolute;
						height: 3vh;
						line-height: 3vh;
						width: 100vw;
						text-align: center;
					}

					.feedbackText {
						top: 4vh;
						left: 3vw;
						position: absolute;
						height: 4vh;
						width: 64vw;
						border-bottom: 1rpx red solid;
					}

					.feedbackButton {
						position: absolute;
						height: 4vh;
						width: 24vw;
						top: 5vh;
						left: 72vw;
					}
				}
			}
		}
	}
</style>