<template>
	<view class="mainList3">
		<view class="mar"></view>
		<view class="swipercontain">
			<view class="innerswipercontain">
				<u-swiper style="swiper" :list="list3" previousMargin="72" nextMargin="72" acceleration circular
					:autoplay="true" radius="5" bgColor="#273333" @click="clic(index)" :effect3d="true"></u-swiper>
			</view>
		</view>
		<view class="gongneng1">
			<u-button type="primary" class="innergongneng1" @click="baojing">
				<u-icon name="bell" class="u-icon" size="34" custom-style="margin:0rpx auto"></u-icon>
				<view class="tips">报警</view>
				<view class="explain">警察联系服务</view>
			</u-button>
			<u-button type="primary" class="innergongneng1" @click="toxiangxixinxi()">
				<u-icon name="bookmark" class="u-icon" size="34" custom-style="margin:0rpx auto"></u-icon>
				<view class="tips">信息</view>
				<view class="explain">扶梯详情信息</view>
			</u-button>
			<u-button type="primary" class="innergongneng1" @click="weixiu">
				<u-icon name="warning" class="u-icon" size="34" custom-style="margin:0rpx auto"></u-icon>
				<view class="tips">报修</view>
				<view class="explain">部件维护情况</view>
			</u-button>
			<u-button type="primary" class="innergongneng1" @click="toList2Copy()">
				<u-icon name="map" class="u-icon" size="34" custom-style="margin:0rpx auto"></u-icon>
				<view class="tips">定位</view>
				<view class="explain">获取您的位置</view>
			</u-button>
			<view class="gongneng1Biaoyu" :style="ggby2" @click="togengxin()">{{xiaoxitongzhi}}</view>
		</view>
		<view class="gongneng2" @click="tianyi">
			<image src="../../static/futianquan9.jpg" mode=""></image>
		</view>
		<view class="gongneng3">
			<view class="gg3partion gg3mar" @click="tojiankong"><u-icon class="arrow-left" name="arrow-left"
					size="24"></u-icon>
				实况监控</view>
			<view class="gg3partion gg3right" @click="tolianxiwomen(e=1)"><u-icon class="arrow-right" name="arrow-right"
					size="24"></u-icon>
				个人信息</view>
			<view class="gg3partion gg3botton" @click="tonews">近期新闻</view>
			<view class="gg3partion gg3mar gg3botton" @click="toxiangxixinxi()">故障记录</view>
		</view>
	</view>
</template>

<script>
	import text from '../../uni_modules/uview-ui/libs/config/props/text';
	export default {
		data() {
			return {
				index: 10,
				ipc: "",
				weixiudidian: '',
				list3: [
					'../../static/beijing21.jpg',
					'../../static/futianquan5.jpg',
					'../../static/futianquan12.jpg',
				],
				fun: 200,
				setInterval1: null,
				xiaoxitongzhi: "~扶梯智能安防系统3.0马上更新，快来了解详情吧~",
			}
		},
		computed: {
			ggby2() {
				return {
					textIndent: this.fun + "px"
				}
			},
		},
		onShow() {
			let that = this;
			this.setInterval1 = setInterval(function() {
				that.fun -= 1
				if (that.fun <= -500) {
					that.fun = 500
				}
			}, 10)
		},
		onHide() {
			clearInterval(this.setInterval1)
			this.fun = -200
		},
		methods: {
			toList2Copy() {
				uni.navigateTo({
					url: "/pages/list1/list1Exchange/list1Exchange"
				})
			},
			toxiangxixinxi() {
				uni.navigateTo({
					url: '/pages/xaingxixinxi/xaingxixinxi',
					success() {
						console.log(1);
					}
				})
			},
			clic(index) {
				console.log(index);
			},
			tianyi() {
				uni.showModal({
					title: "注意危险,\n安全第一!",
					content: '',
					showCancel: false,
					cancelText: '收到',
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			},
			tonews() {
				uni.navigateTo({
					url: '/pages/news/news',
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			},
			tofuwu() {
				uni.navigateTo({
					url: '/pages/tuli/tuli'
				})
			},
			togengxin() {
				uni.navigateTo({
					url: '/pages/shezhi/shezhi',
					success() {
						console.log('跳转至设置界面');
					}
				})
			},
			baojing() {
				uni,
				uni.getLocation({
					type: 'wgs84',
					geocode: 'true',
					success: function(res) {
						console.log(res)
					},
				});
				uni.showModal({
					title: '请求已收到',
					content: '',
					showCancel: false,
					success: () => {}
				});
			},
			weixiu() {
				uni.navigateTo({
					url: '/pages/list1/weixiu/weixiu',
					success() {
						console.log("跳转至维修页面");
					},
					fail() {
						console.log("跳转至维修页面失败");
					}
				})
			},
			tojiankong() {
				uni.switchTab({
					url: "/pages/list2/list2",
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			},
			tolianxiwomen(e) {
				uni.switchTab({
					url: '/pages/list3/list3',
					success() {
						if (e === 2) {
							uni.setStorageSync('shezhi', e);
							console.log("跳转至个人信息页面中的设置页面");
						} else {
							uni.clearStorageSync("shezhi");
							console.log("跳转至个人信息页面");
						}
					},
					fail() {
						console.log("跳转至个人信息页面失败");
					}
				})
			},
		},
		onLoad() {},
	}
</script>

<style lang="scss" scoped>
	.mainList3 {
		height: 100vh;
		width: 100vw;
		background-image: linear-gradient(to bottom, #242c2f, #616e72);

		.mar {
			height: 3vh;
			background-color: #273333;
			position: relative;
		}

		.swipercontain {
			height: 24vh;
			border: 1rpx gray solid;
			background-color: #273333;

			.innerswipercontain {
				width: 100%;
				height: 20vh;
				margin: 20rpx auto;
			}

			.swiper {}
		}

		.gongneng1 {
			width: 100%;
			height: 16vh;
			margin: 1vh auto;
			border: 1rpx gray solid;
			position: relative;

			.gongneng1Biaoyu {
				float: left;
				bottom: 0%;
				position: absolute;
				overflow: hidden;
				display: block;
				height: 2vh;
				line-height: 2vh;
				width: 100%;
				font-style: italic;
				font-weight: 300;
				color: #4a6887;
				font-size: 20rpx;
			}

			.innergongneng1 {
				opacity: 0.9;
				width: 150rpx;
				height: 10vh;
				opacity: 0.8;
				background-image: linear-gradient(to top, #4a6887, #3498db);
				// background-color: #3498db;
				border: 3rpx black solid;
				border-radius: 24rpx;
				margin-top: 1vh;
				margin-left: 30rpx;
				float: left;
				position: relative;
				box-shadow: 0rpx 0rpx 2rpx white;
				text-align: center;

				.u-icon {
					margin: auto 0rpx;
					margin-top: 0vh;
				}

				.tips {
					height: 2vh;
					line-height: 5vh;
					font-size: 24rpx;
					bottom: 0;
					width: 100%;
					bottom: 4vh;
					position: absolute;
					color: black;
					font-weight: 700;
				}

				.explain {
					width: 100%;
					height: 4vh;
					text-align: 4vh;
					line-height: 5vh;
					position: absolute;
					bottom: 0rpx;
					font-size: 18rpx;
					font-weight: 300;
					overflow: hidden;
					color: black;
				}
			}
		}

		.gongneng2 {
			width: 640rpx;
			height: 16vh;
			margin: 20rpx auto;
			border: 1rpx red solid;
			border: red;
			border-radius: 48rpx;
			z-index: 22;

			image {
				opacity: 0.9;
				width: 100%;
				height: 100%;
			}
		}

		.gongneng3 {
			width: 720rpx;
			margin: 0rpx auto;

			.gg3partion {
				width: 240rpx;
				border: 1rpx black solid;
				float: left;
				margin-left: 80rpx;
				margin-top: 20rpx;
				border-radius: 64rpx;
				text-align: center;
				line-height: 12vh;
				color: black;
				background-color: #4e8bb8;
				box-shadow: 0rpx 0rpx 4rpx skyblue;
			}

			.gg3mar {
				margin-left: 80rpx;
			}

			.arrow-left {
				float: left;
				margin-top: 4vh;
			}

			.arrow-right {
				float: right;
				margin-top: 4vh;
			}

		}
	}
</style>