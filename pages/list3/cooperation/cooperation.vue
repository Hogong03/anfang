<template>
	<view id="root">
		<view class="mar" style="height: 10vh;"></view>
		<view class="lianxiwomen">
			<ul>
				<li class="topli">邮箱：</li>
				<li>www.baidu.com</li>
				<li class="topli">微信：</li>
				<li>weixin</li>
				<li class="topli">电话</li>
				<li>10086</li>
			</ul>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		methods: {

		}
	}
</script>

<style lang="scss">
	#root {
		background-color: #dcdfe6;
		height: 100vh;
		width: 100vw;

		.lianxiwomen {
			ul {

				li {
					margin: 0rpx auto;
					width: 80vw;
					height: 8vh;
					line-height: 8vh;
					text-align: center;
					border: 1px #8b8687 solid;
					border-radius: 24rpx;
					font-size: 3vh;
					user-select: all;
				}

				.topli {
					border: 0rpx;
					user-select: none;
					color: #989cab;
				}
			}
		}
	}
</style>