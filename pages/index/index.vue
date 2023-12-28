<template>
	<view id="root">
		<view class="mar1"></view>
		<view class="title" :style="height">智能安防系统</view>
		<view class="mar2" :style="marginHeight"></view>
		<view class="backgroundImage">
			<u-button class="tologin changeButton" @click="tologin()">登录</u-button>
			<view class="tozhuce changeButton" @click="toregister()">没有账户？联系我们</view>
		</view>
	</view>
</template>

<script>
	import color from '../../uni_modules/uview-ui/libs/config/color'
	export default {
		data() {
			return {
				drop: 1000,
				timeID: "",
				timeID2: "",
				showdrop: true,
				enter: true,
				openOrNot: true,
				drop2: 88,
			}
		},
		methods: {
			tologin() {
				const that = this
				if (this.enter) {
					that.timeID2 = setInterval(function() {
						if (that.drop2 > 5 && that.drop >= 5) {
							that.drop2 -= 0.5
							that.drop -= 2
						} else {
							clearInterval(that.timeID2);
							uni.switchTab({
								url: "/pages/list1/list1Exchange/list1Exchange"
							})
						}
					}, 1)
				} else {
					uni.navigateTo({
						url: "/pages/login/login",
						success() {
							console.log("跳转至登陆界面");
						}
					})
				}
			},
			toregister() {
				uni.navigateTo({
					url: "/pages/login/register/register",
					success() {
						console.log("跳转至注册页面");
					}
				})
			}
		},
		computed: {
			height() {
				return {
					top: this.drop + "rpx"
				}
			},
			marginHeight() {
				return {
					height: this.drop2 + "vh"
				}
			}
		},
		onShow() {
			const that = this
			if (this.openOrNot) {
				this.timeID = setInterval(function() {
					if (that.drop >= 240) {
						that.drop -= 2;
					}
					if (that.drop2 >= 56) {
						that.drop2 -= 0.1
					}
					if (that.drop <= 240 && that.drop2 <= 56) {
						console.log("停止计时器");
						clearInterval(that.timeID)
					}
				}, 1);
				this.openOrNot = !this.openOrNot
			}
		},
		onHide() {
			if (!this.openOrNot) {
				clearInterval(this.timeID);
			}
		}
	}
</script>

<style lang="scss">
	#root {
		height: 100vh;
		width: 100vw;
		background: url("../../static/beijing20.jpg") no-repeat 100% 100%;
		background-size: cover;
		position: relative;
		background-color: #252525;
		position: relative;
		overflow: hidden;

		.mar1 {
			height: 20vh;
		}

		.title {
			text-align: center;
			font-size: 64rpx;
			text-shadow: 0rpx 0rpx 4rpx gray;
			width: 100vw;
			opacity: 0.9;
			position: absolute;
			height: 6vh;
			line-height: 6vh;
			color: #f3f4f6;
			text-shadow: 0rpx 12rpx 16rpx #252525;
		}

		.backgroundImage {

			.changeButton {
				margin: 0rpx auto;
				height: 4vh;
				line-height: 4vh;
				width: 42vw;
				color: white;
				text-align: center;
				color: #d0d1d2;
				opacity: 0.8;
				margin-bottom: 2rpx;
				border-radius: 12rpx;
			}

			.tologin {
				color: #000000;
				border: black solid 1rpx;
				box-shadow: 0rpx 0rpx 4rpx gray;
				background-image: linear-gradient(to top, #E6DADA, #274046);
			}

			.tozhuce {
				opacity: 0.6;
			}
		}
	}
</style>