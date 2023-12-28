<template>
	<view class="">
		<view class="" v-for="item in uButton" :key="item.id">
			<u-button :type=item.type @click="uButtonClick(item.id)">{{item.detail}}</u-button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				uButton: [{
					id: 1,
					detail: "扶梯速度",
					type: "primary",
				}, {
					id: 2,
					detail: "扶梯人数",
					type: "primary",
				}, {
					id: 3,
					detail: "扶梯温度",
					type: "primary",
				}, {
					id: 4,
					detail: "载重情况",
					type: "primary",
				}, {
					id: 5,
					detail: "安全按钮",
					type: "primary",
				}, {
					id: 6,
					detail: "扶手状态",
					type: "primary",
				}, ]
			}
		},
		methods: {
			uButtonClick(e){
				console.log(e);
			}
		}
	}
</script>

<style lang="scss">

</style>