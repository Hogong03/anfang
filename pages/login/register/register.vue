<template>
	<view id="root">
		<view class="comeBack" @click="comeBack()">
			<u-icon class="comeBackButton" name="arrow-left" color="#c0c4cc" @click="comeBack()" size="24"></u-icon>
		</view>
		<view class="welcomeRegister">欢迎注册</view>
		<view class="form">
			<form @submit="formSubmit">
				<view class="formInput">
					<span>手机号:</span><input type="telphone" name="tel" placeholder="请输入手机号" />
				</view>
				<view class="formInput">
					<span>密码:</span><input type="safe-password" name="password" placeholder="请输入密码" />
				</view>
				<view class="formInput">
					<span>确定密码:</span><input type="safe-password" name="passwordMakeSure" placeholder="请再次输入密码" />
				</view>
				<view class="formInput">
					<span>邀请码:</span><input type="text" name="invitation" placeholder="请输入邀请码" />
				</view>
				<view class="uni-btn-v">
					<button form-type="submit" size="mini" @click="formSubmit(e)">Submit</button>
				</view>
			</form>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {}
		},
		methods: {
			comeBack() {
				console.log(1);
				uni.navigateTo({
					url: "/pages/login/login",
					success() {
						console.log("跳转至登陆界面");
					}
				})
			},

			formSubmit: function(e) {
				console.log('form发生了submit事件，携带数据为：' + JSON.stringify(e.detail.value))
				var formdata = e.detail.value
				console.log(JSON.stringify(formdata));
			},
		}
	}
</script>

<style lang="scss">
	#root {
		background: url("../../../static/beijing20.jpg") no-repeat 100% 100%;
		height: 100vh;
		width: 100vw;
		background-size: cover;
		background-color: #252525;
		position: relative;

		.comeBack {
			width: 36vw;
			color: white;
			font-size: 8rpx;
			position: absolute;
			top: 4vh;
		}

		.welcomeRegister {
			text-align: center;
			height: 32vh;
			line-height: 32vh;
			text-align: center;
			font-size: 64rpx;
			width: 100vw;
			opacity: 0.9;
			color: #9b9da4;
			text-shadow: 0rpx 0rpx 6rpx aqua;
		}

		.form {
			width: 72vw;
			margin: 0rpx auto;
			height: 36vh;
			opacity: 0.6;
			border: 1rpx #adb6bf solid;
			border-radius: 20rpx;
			box-shadow: 0rpx 0rpx 24rpx gray;
			justify-content: space-between;
			background-color: #d3e6f1;

			form {
				.formInput {
					height: 6vh;
					width: 100%;
					margin-top: 12rpx;
					line-height: 6vh;

					span {
						display: block;
						float: left;
						width: 24vw;
						height: 100%;
						text-indent: 1em;
					}

					input {
						height: 90%;
						border-bottom: gray 1rpx solid;
						width: 42vw;
					}

				}

				.uni-form-item .title {
					padding: 20rpx 0;
				}

				.uni-btn-v {
					opacity: 0.6;
					margin: 0rpx auto;

					button {
						height: 3vh;
						line-height: 3vh;
						width: 24vw;
						margin: 24rpx auto;
						display: block;
					}
				}
			}
		}
	}
</style>