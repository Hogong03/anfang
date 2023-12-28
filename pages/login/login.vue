<template>
	<!-- 主页面 -->
	<view id="root">
		<!-- 页面空格（调整间距） -->
		<view class="mar"></view>
		<!-- 登录页面 -->
		<view class="navtitle">{{ title }}</view>
		<view id="mainbody">
			<view class="form">
				<!-- 登录表单 -->
				<form @submit="onsubmit()">
					<!-- 账号输入框 -->
					<view class="input_admin">
						<input type="text" placeholder="请输入账号或者手机号" v-model="admin">
					</view>
					<!-- 密码输入框 -->
					<view class="input_password">
						<input type="password" placeholder="请输入密码" v-model="password">
					</view>
					<!-- 登录按钮 -->
					<view class="butDL">
						<button form-type="submit" size="default" type="primary"
							style="height: 80rpx; line-height: 80rpx;">登录</button>
					</view>
					<view class="butJZ">
						<label>
							<checkbox :checked="jizhumima" @click="jiZhu" /><text>记住密码</text>
						</label>
					</view>
				</form>
				<!-- 切换到注册页面 -->
				<view class="butZC">
					<button form-type="submit" size="mini" class="zhucce" @click="handleRegister()">注册</button>
				</view>
				<!-- <view class="passwordFindBack" @click="passwordFindBack()">找回密码</view> -->
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		// 数据
		data() {
			return {
				title: "智能安防系统",
				admin: '',
				password: '',
				jizhumima: true,
			};
		},
		onLoad() {},
		// 函数
		methods: {
			// 切换页面
			handleRegister() {
				uni.navigateTo({
					url: "/pages/login/register/register",
					success() {
						console.log("跳转至注册页面");
					}
				})
			},
			// 登录提交
			onsubmit(e) {
				// 登录成功
				// uni.request({
				// 	url: "http://192.168.12.32:8080/sys/login?username=zs&password=123456",
				// 	method: "POST",
				// 	header: {
				// 		"Content-Type": "application/x-www-form-urlencoded"
				// 	},
				// 	success: function(res) {
				// 		console.log(1);
				// 		console.log(res.data);
				// 		console.log(2);
				// 		if (res) {
				// 			console.log("登陆成功");
				// 		} else {
				// 			console.log("登陆失败");
				// 		}
				// 	},
				// })
				uni.setStorageSync("remuberPassword", this.jizhumima)
				uni.switchTab({
					url: '/pages/list1/list1',
					success() {
						console.log('登录成功');
					}
				});
				let PW = uni.$u.trim(this.passwordd);
				let AD = uni.$u.trim(this.adminn)
				if (PW == '123456' && AD == 'admin') {
					if (this.jizhumima) {
						console.log('记住密码');
						uni.setStorageSync('admin', this.adminn);
						uni.setStorageSync('password', this.passwordd);
					} else {
						console.log('不记住密码');
						uni.removeStorageSync('admin')
						uni.removeStorageSync('password')
						this.adminn = ''
						this.passwordd = ''
					}
					uni.showLoading({
						title: '登陆中',
						success() {
							setTimeout(function() {
								uni.hideLoading()
								uni.switchTab({
									url: '/pages/list1/list1',
									success() {
										console.log('登录成功');
									}
								});
							}, 500);
						}
					})
					// 账号或者密码为空
				} else if (this.passwordd === '' || this.adminn === '') {
					uni.showToast({
						title: '请输入账号或者密码',
						icon: "error",
					})
				}
				// 账号或者密码错误
				else {
					uni.showToast({
						title: '账号或者密码错误',
						icon: "error"
					})
				}
			},
			jiZhu() {
				this.jizhumima = !this.jizhumima
			},
			passwordFindBack() {
				uni.navigateTo({
					url: "/pages/login/passwordFindBack/passwordFindBack",
					success() {
						console.log("跳转至找回密码界面");
					}
				})
			}
		},
		mounted() {
			const username = uni.getStorageSync('adminn')
			const password = uni.getStorageSync('passowrdd')
		},
		onShow() {
			if (this.jizhumima) {
				console.log('记住密码');
				this.adminn = uni.getStorageSync('admin');
				this.passwordd = uni.getStorageSync('password')
			} else {
				console.log('不记住密码');
				uni.removeStorageSync('admin')
				uni.removeStorageSync('password')
				this.adminn = ''
				this.passwordd = ''
			}
		}
	}
</script>

<!-- SCSS样式 -->
<style lang="scss" scoped>
	#root {
		height: 100vh;
		width: 100vw;
		background: url("../../static/beijing20.jpg") no-repeat 100% 100%;
		background-size: cover;
		background-color: #252525;

		.mar {
			width: 100vw;
			height: 240rpx;
		}

		.navtitle {
			font-size: 64rpx;
			text-align: center;
			color: #82848a;
			text-shadow: 0rpx 0rpx 2rpx aqua;
		}

		#mainbody {
			opacity: 0.6;
			width: 600rpx;
			height: 480rpx;
			border: 1rpx #adb6bf solid;
			margin: 120rpx auto;
			text-align: center;
			border-radius: 24rpx;
			box-shadow: 0rpx 0rpx 24rpx gray;
			justify-content: space-between;
			background-color: #d3e6f1;

			.form {
				position: relative;

				.input_password,
				.input_admin {
					height: 72rpx;
					width: 480rpx;
					border: 1rpx #045d75 solid;
					box-shadow: 0rpx 0rpx 4rpx black;
					margin: 48rpx auto;
					border-radius: 18rpx;
					line-height: 180rpx;
					font-size: 64rpx;

					input {
						height: 100%;
						font-size: 40rpx;
					}
				}

				.butDL {
					width: 320rpx;
					margin: 0rpx auto;
				}

				.butZC {
					width: 320rpx;
					margin: 20rpx auto;

					.zhucce {
						height: 40rpx;
						line-height: 40rpx;
						background-color: transparent;
						color: #888;
					}
				}

				.passwordFindBack {
					height: 48rpx;
					line-height: 48rpx;
					border: 1rpx #909399 solid;
					width: 20vw;
					position: absolute;
					right: 0;
					bottom: -3vh;
					border-radius: 8rpx;
				}

				.butJZ {
					float: right;
					margin-top: -124rpx;
					margin-right: 60rpx;
				}

			}
		}
	}
</style>