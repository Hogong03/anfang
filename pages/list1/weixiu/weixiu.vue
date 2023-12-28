<template>
	<view class="mian">
		<view class="miancontain">
			<view class="">扶梯部件</view>
			<view class=""><input type="" placeholder="搜索" v-model="sousuo" /></view>
			<button @click="sousou()">确定</button>
			<ul v-for="item in subXiangqing" :key="item.id">
				<li>
					<view class="container">
						<view class="URL">
							<image :src=item.URL mode=""></image>
						</view>
						<view class="name"><span style="font-weight: 700;">部件名：</span> {{item.name}}</view>
						<view class="jieshi">
							年龄：{{item.age}}<br>
							介绍: {{item.jieshi}}<br>
							维修次数: {{item.maintenanceRequency}}
						</view>
					</view>
				</li>
			</ul>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				sousuo: "1",
				subXiangqing: "",
				xiangqing: [{
						id: 1,
						name: '桁架',
						URL: "../../../static/futibujian1.jpg",
						jieshi: "部件1",
						age: "10年",
						maintenanceRequency: 10 + "次"
					},
					{
						id: 2,
						name: "驱动机",
						URL: "../../../static/futibujian2.jpg",
						jieshi: "部件2",
						age: "8年",
						maintenanceRequency: 10 + "次"
					},
					{
						id: 3,
						name: "驱动装置",
						URL: "../../../static/futibujian3.jpg",
						jieshi: "部件3",
						age: "4年",
						maintenanceRequency: 10 + "次"
					},
					{
						id: 4,
						name: "张紧装置",
						URL: "../../../static/futibujian4.jpg",
						jieshi: "部件4",
						age: "6年",
						maintenanceRequency: 10 + "次"
					},
					{
						id: 5,
						name: "导轨",
						URL: "../../../static/futibujian5.jpg",
						jieshi: "部件5",
						age: "1年",
						maintenanceRequency: 10 + "次"
					},
					{
						id: 6,
						name: "梯级链",
						URL: "../../../static/futibujian6.jpg",
						jieshi: "部件6",
						age: "5月",
						maintenanceRequency: 10 + "次"
					},
				]
			};
		},
		methods: {
			sousou() {
				const that = this
				console.log(that.sousuo);
				var arr = this.xiangqing.filter(function(item, value) {
					console.log(item.name);
					return item.id == that.sousuo || item.name.includes(that.sousuo)
				})
				console.log(arr);
				this.subXiangqing = arr
			}
		},
		onLoad() {
			this.subXiangqing = this.xiangqing
		}
	}
</script>

<style lang="scss">
	.mian {
		background-color: #dedfe6;

		.miancontain {
			margin: 0rpx auto;

			ul {
				margin: 10rpx auto;

				li {
					.container {
						height: 16vh;
						width: 100%;
						margin: 0rpx auto;
						background-size: cover;

						.URL {
							width: 32%;
							height: 16vh;
							float: left;
							border: 1rpx gray solid;

							image {
								height: 100%;
								width: 100%;
							}
						}

						.name {
							width: 62%;
							height: 4vh;
							float: left;
							border: 1rpx gray solid;
						}

						.jieshi {
							width: 62%;
							height: 12vh;
							float: left;
							border: 1rpx gray solid;
							overflow: scroll;
						}
					}
				}
			}
		}
	}
</style>