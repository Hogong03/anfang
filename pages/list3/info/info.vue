<template>
	<view id="root">
		<view class="mar" style="height: 3vh;"></view>
		<view class="information">
			<ul v-for="item in informations" :key="item.id">
				<li @click="toFunction(item.id)">
					<view class="image">
						<image src="../../../static/developer.png"></image>
					</view>
					<view class="title">
						{{item.title}}
					</view>
					<view class="context">
						{{item.context}}
					</view>
					<view class="time">
						{{item.time}}
					</view>
					<view class="tag">
						未读
					</view>
				</li>
			</ul>
		</view>
		<view class="clearAll">
			<u-button @click="clearAll()" type="info" plain="" shape="circle">清除所有消息</u-button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				informations: [{
					id: 1,
					title: "APP开发者",
					context: "智能安防系统最新版本发布了",
					time: "11.6 20:50"
				}, {
					id: 2,
					title: "APP开发者",
					context: "智能安防系统最新版本发布了",
					time: "11.7 20:50"
				}, {
					id: 3,
					title: "APP开发者",
					context: "智能安防系统最新版本发布了",
					time: "11.8 20:50"
				}, ]
			};
		},
		methods: {
			toFunction(e) {
				console.log(e);
			},
			clearAll() {
				this.informations = ""
			}
		}
	}
</script>

<style lang="scss">
	#root {
		background-color: #f3f4f6;
		height: 100vh;
		width: 100vw;

		.information {

			ul {
				li {
					height: 10vh;
					width: 100vw;
					border: 1rpx gray solid;
					margin-top: 2vh;
					position: relative;
					border-radius: 12rpx;

					.image {
						float: left;
						height: 7.2vh;
						width: 7.2vh;
						margin-top: 1.4vh;
						margin-left: 1.4vh;
						position: absolute;
						border-radius: 7.2vh;
						overflow: hidden;
						box-shadow: 0rpx 0rpx 4rpx #252525;

						image {
							height: 100%;
							width: 100%;
						}
					}

					.title {
						height: 4vh;
						line-height: 4vh;
						font-weight: 700;
						font-size: 28rpx;
						position: absolute;
						top: 1vh;
						left: 18vw;
					}

					.context {
						height: 3vh;
						line-height: 3vh;
						font-size: 20rpx;
						font-weight: 300;
						position: absolute;
						top: 5vh;
						left: 18vw;
					}

					.time {
						float: right;
						position: absolute;
						top: 1vh;
						right: 2vw;
						font-size: 18rpx;
						font-weight: 300;
					}

					.tag {
						position: absolute;
						right: 2vw;
						bottom: 2vh;
						font-size: 20rpx;
						width: 12vw;
						text-align: center;
						height: 3vh;
						line-height: 3vh;
						border: gray solid 1rpx;
						border-radius: 12rpx;
					}
				}
			}
		}

		.clearAll {
			height: 4vh;
			width: 36vw;
			position: fixed;
			top: 64vh;
			left: 32vw;
		}
	}
</style>