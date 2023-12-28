<template>
	<view class="userInformation">
		<view class="mar"></view>
		<view class="yonghuxinxi" v-for="p in uservaluermation" :key="p.id">
			<view class="information" @click="toInfo(p.id)">
				<view class="infoName">{{p.name}}</view>
				<view class="infoValue">{{p.value}}</view>
				<view class="extension">
					<image src="../../../static/arrow-left-black.png" mode=""></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				uservaluermation: [{
						id: 1,
						name: '名称:',
						value: 'Julien'
					},
					{
						id: 2,
						name: '呢称:',
						value: 'Dantes'
					},
					{
						id: 3,
						name: '电话:',
						value: '10086'
					},
					{
						id: 4,
						name: '地点:',
						value: 'NIT'
					},
				],
			}
		},
		methods: {
			toInfo(e) {
				console.log(1);
				if (e <= 3) {
					let s = --e
					uni.showModal({
						title: "请输入新的",
						editable: true,
						success: (res) => {
							if (res.content != "") {
								console.log(res.content);
								this.uservaluermation[s].value = res.content
							} else {
								uni.showToast({
									title: "无效的值",
									icon: "error",
								})
							}
						}
					})
				} else if (e === 4) {
					uni.showToast({
						title: "更改地点请联系管理员",
						icon: "error"
					})
				}
			}
		}
	}
</script>

<style lang="scss">
	.userInformation {
		height: 90vh;
		width: 100vw;
		background-color: #dcdfe6;

		.mar {
			height: 2vh;
		}

		.yonghuxinxi {
			background-color: #f3f4f6;
			margin-bottom: 1vh;
			height: 6vh;
			line-height: 6vh;
			text-indent: 1em;
			font-size: 28rpx;

			.infoName {
				width: 40%;
				float: left;
			}

			.infoValue {
				float: left;
				text-align: right;
				width: 52%;
				float: left;
				height: 6vh;
			}

			.extension {
				width: 6%;
				margin-right: 2%;
				height: 3.6vh;
				margin-top: 1.2vh;
				float: left;

				image {
					height: 100%;
					width: 100%;
				}
			}
		}
	}
</style>