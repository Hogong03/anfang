<template>
	<view class="setting">
		<view class="">当前版本:{{versionInfo}}</view>
		<view class="">版本信息:</view>
		<view class="versionInfo">
			当前版本为智能安防系统2.01<br/>
			更新内容：<br>
			1.优化了页面设计<br>
			2.增添了新功能<br>
			3.优化了内存<br>
			请大家尽快更新到最新版本
		</view>
		<view class="uButton">
			<u-button size="mdeium" class="custom-style" type="primary">检查版本更新</u-button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				versionInfo: "智能安防系统2.01"
			}
		},
		methods: {

		},
		onLoad() {
		}
	}
</script>

<style lang="scss">
	.setting {
		background-color: #f3f4f6;
		height: 100vh;
		width: 100vw;
		.uButton {
			width: 68vw;
			margin: 20vh auto;
		}
		.versionInfo{
			text-indent: 1em;
		}
	}
</style>