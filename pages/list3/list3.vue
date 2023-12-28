<template>
	<view id="root">
		<view class="list3FunctionMar"></view>
		<view class="list3Function1">
			<view class="list3Function1Icon">
				<image src="../../static/GGB.jpg" mode=""></image>
			</view>
			<view class="list3Function1Name">Hello!{{myName}}</view>
			<view class="list3Function1Number">扶梯数:{{escalatorNumber}}</view>
			<view class="list3Function1Information">
				<view class="imageBell">
					<u-icon name="bell" @click="toInfo(Information)" :color="redOrWhite"></u-icon>
				</view>
				<view class="BellNumber" :style="disappearOrnot">{{Information}}</view>
			</view>
			<view class="list3Function1Condition">{{escalatorCondition}}</view>
			<view class="list3FunctionTitle">智能安防，为您保驾护航!</view>
			<view class="notification" :style="textRoll" @click="toUpdata()">~智能安防系统3.0马上更新，快来了解详情吧~</view>
		</view>
		<view class="list3Function2">
			<ul v-for="item in list3Function2" :key="item.id">
				<li>
					<view class="list3Function2Image">
						<image :src=item.src></image>
					</view>
					<view class="list3Function2Value">{{item.value}}</view>
				</li>
			</ul>
		</view>
		<view class="list3Function3">
			<ul v-for="item in list3Function3" :key=item.id>
				<li @click="list3Function3s(item.id)">
					<view class="u-icon">
						<image :src=item.iconSrc>
						</image>
					</view>{{item.value}}
					<view class="image-arrow">
						<image :src=item.arrowSrc></image>
					</view>
				</li>
			</ul>
		</view>
		<view class="list3Button">
			<view @click="toLogin()" type="primary" shape="square" :ripple="true" size="mini">返回登陆</view>
		</view>
	</view>
</template>

<script>
	import color from '../../uni_modules/uview-ui/libs/config/color'
	export default {
		data() {
			return {
				escalatorNumber: 2,
				Information: 1,
				escalatorCondition: "一切状态正常",
				myName: "Julien",
				list3Function2: [{
					id: 1,
					value: "扶梯信息",
					src: "../../static/escalator/escalator.png"
				}, {
					id: 2,
					value: "故障记录",
					src: "../../static/history.png",
				}, {
					id: 3,
					value: "增添扶梯",
					src: "../../static/add-escalator.png",
				}, {
					id: 4,
					value: "我的订单",
					src: "../../static/oeder.png"
				}, ],
				list3Function3: [{
					id: 1,
					iconSrc: "../../static/zhanghao.png",
					value: "我的信息",
					arrowSrc: "../../static/arrow-left.png",
				}, {
					id: 2,
					iconSrc: "../../static/escalator.png",
					value: "与我们合作",
					arrowSrc: "../../static/arrow-left.png",
				}, {
					id: 3,
					iconSrc: "../../static/feedback.png",
					value: "反馈信息",
					arrowSrc: "../../static/arrow-left.png",
				}, {
					id: 4,
					iconSrc: "../../static/setting.png",
					value: "版本更新",
					arrowSrc: "../../static/arrow-left.png",
				}, ],
				roll: -200,
				timeId: "",
			}
		},
		methods: {
			toInfo(e) {
				uni.navigateTo({
					url: "/pages/list3/info/info",
					success() {
						console.log("跳转至信息页面")
					},
					fail() {
						console.log("跳转失败")
					}
				})
			},
			toLogin() {
				uni.navigateTo({
					url: "/pages/login/login"
				})
			},
			toUpdata() {
				uni.navigateTo({
					url: "/pages/list3/versionUpdata/versionUpdata"
				})
			},
			list3Function3s(e) {
				switch (e) {
					case 1:
						uni.navigateTo({
							url: "/pages/list3/userInformation/userInformation"
						})
						break;
					case 2:
						uni.navigateTo({
							url: "/pages/list3/cooperation/cooperation"
						})
						break;
					case 3:
						uni.navigateTo({
							url: "/pages/list3/feedBack/feedBack"
						})
						break;
					case 4:
						uni.navigateTo({
							url: "/pages/list3/versionUpdata/versionUpdata"
						})
						break;
					default:
						break;
				}
			}
		},
		computed: {
			disappearOrnot() {
				return {
					display: this.Information === 0 ? "none" : "block",
					color: "red"
				}
			},
			redOrWhite() {
				return this.Information === 0 ? "white" : "red"
			},
			textRoll() {
				return {
					textIndent: this.roll + "px"
				}
			}
		},
		onShow() {
			let that = this;
			this.setInterval1 = setInterval(function() {
				that.roll -= 1
				if (that.roll <= -500) {
					that.roll = 500
				}
			}, 8)
		},
		onHide() {
			clearInterval(this.setInterval1)
			this.fun = -200
		},
	}
</script>

<style lang="scss">
	#root {
		height: 100vh;
		width: 100vw;
		background-image: linear-gradient(to bottom, #242c2f, #616e72);
		color: #c0c4cc;
		background-image: linear-gradient(to right, #141E30, #243B55);
		background-image: linear-gradient(to bottom, #273748, #31475c);
		background-image: linear-gradient(to bottom, #242c2f, #616e72);

		.list3Function1 {
			border: 1rpx gray solid;
			height: 20vh;
			width: 100vw;
			position: relative;
			border-radius: 12rpx;
			background-image: linear-gradient(to bottom, #242c2f, #435257, #606266);
			margin-bottom: 1vh;
			opacity: 0.8;

			.list3Function1Icon {
				position: absolute;
				height: 10vh;
				width: 18vw;
				left: 4vw;
				top: 2vh;
				font-size: 24rpx;
				border-radius: 240rpx;
				overflow: hidden;

				image {
					height: 100%;
					width: 100%;
				}
			}

			.list3Function1Name {
				position: absolute;
				height: 2vh;
				width: 20vw;
				top: 2vh;
				left: 26vw;
				font-size: 48rpx;
			}

			.list3Function1Number {
				position: absolute;
				height: 2vh;
				width: 20vw;
				top: 6vh;
				left: 26vw;
				font-size: 24rpx;
			}

			.list3Function1Information {
				position: absolute;
				height: 2vh;
				line-height: 2vh;
				width: 8vw;
				top: 1vh;
				right: 0vw;

				.imageBell {
					height: 2vh;
					width: 3vw;
					float: left;

					image {
						height: 100%;
						width: 100%;
					}
				}

				.BellNumber {
					position: absolute;
					right: 3vw;
					width: 1vw;
					height: 1vh;
					top: -8rpx;
					font-size: 20rpx;
				}
			}

			.list3Function1Condition {
				position: absolute;
				top: 8vh;
				left: 26vw;
				font-size: 16rpx;
			}

			.list3FunctionTitle {
				position: absolute;
				left: 26vw;
				top: 10vh;
			}

			.notification {
				position: absolute;
				bottom: 0;
				width: 100%;
				height: 2vh;
				line-height: 2vh;
				font-style: italic;
				font-size: 1.2vh;
				overflow: hidden;
			}
		}

		.list3FunctionMar {
			height: 4vh;
		}

		.list3Function2 {
			border: 1rpx gray solid;
			height: 20vh;
			width: 100vw;
			border-radius: 3vh 3vh 12rpx 12rpx;
			background-image: linear-gradient(to bottom, #242c2f, #3f474a);
			opacity: 0.8;
			margin-bottom: 2vh;

			ul {
				li {
					height: 10vh;
					border: gray 1rpx solid;
					width: 20vw;
					float: left;
					margin-left: 4vw;
					margin-top: 5vh;
					border-radius: 20rpx;
					background-color: #242c2f;

					.list3Function2Value {
						height: 2vh;
						width: 100%;
						text-align: center;
						line-height: 2vh;
						font-size: 20rpx;
					}

					.list3Function2Image {
						height: 8vh;
						width: 100%;

						image {
							height: 100%;
							width: 100%;
						}
					}
				}
			}
		}

		.list3Function3 {
			height: 560rpx;
			width: 100vw;

			ul {
				li {
					height: 120rpx;
					width: 100vw;
					border: gray solid 1rpx;
					float: left;
					margin: 10rpx auto;
					line-height: 8vh;
					border-radius: 12rpx;
					background-color: #728b94;
					background-image: linear-gradient(to right, #242c2f, #435257);

					.u-icon {
						float: left;
						width: 52rpx;
						height: 48rpx;
						margin-top: 16rpx;
						margin-left: 16rpx;

						image {
							height: 100%;
							width: 80%;
						}
					}

					.image-arrow {
						float: right;
						width: 64rpx;
						height: 64rpx;
						margin-top: 28rpx;

						image {
							width: 100%;
							height: 100%;
						}
					}
				}
			}
		}

		.list3Button {
			width: 36vw;
			height: 4vh;
			line-height: 4vh;
			margin: 20rpx auto;
			text-align: center;
			border: gray solid 1rpx;
			border-radius: 18rpx;
			background-color: #242c2f;
			opacity: 0.8;
		}
	}
</style>