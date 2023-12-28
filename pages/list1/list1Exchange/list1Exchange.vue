<template>
	<view id="root">
		<view class="mar"></view>
		<view class="title">
			智能安防系统
		</view>
		<view class="subTitle">您的安全顾问</view>
		<view class="swiper">
			<u-swiper style="swiper" :list="list3" previousMargin="72" nextMargin="72" acceleration circular
				:autoplay="true" radius="12" bgColor="#273333" @click="clic()"></u-swiper>
		</view>
		<view class="functions">
			<ul v-for="item in funcctions" :key=item.id>
				<li @click="escalatorsFunction(item.id)">
					<view class="functiongImage">
						<image :src=item.src mode=""></image>
					</view>
					<view class="functionName">{{item.functionName}}</view>
				</li>
			</ul>
		</view>
		<view class="fuctions2">
			<view class="fuction21" @click="function21()">功能1</view>
			<view class="fuction22" @click="function22()">功能2</view>
		</view>
		<view class="myEscalators">
			<view class="myEscalatorsTitle">我的扶梯</view>
			<ul v-for="item in myEscalators" :key="item.id">
				<li @click="myEscalatorsFunction(item.id)">
					<view class="location">{{item.location}}</view>
					<view class="runTime">{{item.runTime}}</view>
					<view class="securityFactor">{{item.securityFactor}}</view>
					<view class="escalatorImage">
						<image src="../../../static/beijing21.jpg" mode=""></image>
					</view>
				</li>
			</ul>
			<view class="noMore">---没有更多扶梯---</view>
		</view>
		<view class="mar"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list3: [
					'../../../static/beijing21.jpg',
					'../../../static/beijing21.jpg',
					'../../../static/beijing21.jpg',
				],
				myEscalators: [{
					id: 1,
					location: "润园",
					securityFactor: "safe",
					runTime: 10 + "H"
				}, {
					id: 2,
					location: "沁园",
					securityFactor: "safe",
					runTime: 12 + "H"
				}, {
					id: 3,
					location: "沁园",
					securityFactor: "safe",
					runTime: 12 + "H"
				}],
				funcctions: [{
					id: 1,
					functionName: "扶梯信息",
					src: "../../../static/escalator2.png"
				}, {
					id: 2,
					functionName: "扶梯维修",
					src: "../../../static/fix.png"
				}, {
					id: 3,
					functionName: "近期新闻",
					src: "../../../static/news.png"
				}, {
					id: 4,
					functionName: "扶梯定位",
					src: "../../../static/position.png"
				}, ]
			}
		},
		methods: {
			function21() {
				console.log(1);
			},
			function22() {
				console.log(2);
			},
			myEscalatorsFunction(e) {
				console.log(e);
			},
			clic(e) {
				console.log();
			},
			escalatorsFunction(e) {
				switch (e) {
					case 1:
						console.log(1)
						break;
					case 2:
					uni.navigateTo({
						url:"/pages/list1/weixiu/weixiu",
						success() {
							console.log("跳转至维修页面");
						}
					})
						break;
					case 3:
					uni.navigateTo({
						url:"/pages/news/news",
						success() {
							console.log("跳转至新闻页面");
						}
					})
						break;
					case 4:
						console.log(4)
						break;
					default:
						break;
				}
			}
		}
	}
</script>

<style lang="scss">
	#root {
		height: 100vh;
		width: 100vw;
		background-image: linear-gradient(to top, #54666d, #252525);
		overflow: scroll;

		.title {
			height: 4vh;
			line-height: 4vh;
			text-indent: 6vw;
			font-weight: 700;
			font-size: 48rpx;
		}

		.subTitle {
			font-size: 24rpx;
			height: 3vh;
			color: #f3f4f6;
			font-weight: 300;
			text-indent: 6vw;
		}

		.swiper {
			width: 100vw;
			height: 20vh;
			margin: 2vh auto;
			border-radius: 32rpx;
			border: gray 1rpx solid;
			overflow: hidden;
			background-color: #273333;
		}

		.functions {
			border: 1rpx solid gray;
			border-radius: 24rpx;
			background-image: linear-gradient(to bottom, #252525, #363636);
			height: 14vh;
			width: 96vw;
			margin: 4vh 2vw;

			ul {
				li {
					float: left;
					height: 10vh;
					margin-top: 2vh;
					width: 19vw;
					margin-left: 4vw;
					text-align: center;
					border: 1rpx gray solid;
					box-shadow: 0rpx 0rpx 4rpx gray;

					.functiongImage {
						height: 7vh;
						width: 100%;

						image {
							height: 100%;
							width: 100%;
						}
					}

					.functionName {
						height: 3vh;
						width: 100%;
						line-height: 3vh;
						font-size: 20rpx;
					}
				}
			}
		}

		.fuctions2 {
			border: gray solid 1rpx;
			width: 96vw;
			height: 12vh;
			line-height: 10vh;
			margin: 2vh auto;
			border-radius: 36rpx;
			text-align: center;

			.fuction21 {
				height: 10vh;
				width: 42vw;
				margin-left: 4vw;
				float: left;
				border: 1rpx gray solid;
				border-radius: 36rpx;
				margin-top: 1vh;
			}

			.fuction22 {
				height: 10vh;
				width: 42vw;
				margin-left: 4vw;
				float: left;
				border: 1rpx gray solid;
				border-radius: 36rpx;
				margin-top: 1vh;
			}
		}

		.mar {
			height: 4vh;
		}

		.myEscalators {

			ul {
				li {
					display: block;
					height: 12vh;
					width: 100vw;
					margin-top: 1vh;
					border: 1rpx #f3f4f6 solid;
					position: relative;

					.location {
						position: absolute;
						height: 3vh;
						line-height: 3vh;
						left: 6vw;
						top: 0.4vh;
						font-weight: 600;
						font-size: 36rpx;
					}

					.runTime {
						position: absolute;
						left: 6vw;
						top: 6vh;
						height: 3vh;
						line-height: 3vh;
					}

					.securityFactor {
						position: absolute;
						left: 6vw;
						top: 4vh;
						height: 3vh;
						line-height: 3vh;
					}

					.escalatorImage {
						height: 3vh;
						line-height: 3vh;
						position: absolute;
						height: 10vh;
						width: 24vw;
						right: 6vw;
						top: 1vh;
						overflow: hidden;
						border-radius: 36rpx;

						image {
							height: 100%;
							width: 100%;
						}
					}
				}
			}

			.noMore {
				text-align: center;
				color: #f3f4f6;
				font-size: 24rpx;
				opacity: 0.6;
			}
		}
	}
</style>