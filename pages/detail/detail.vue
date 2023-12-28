<template>
	<view>
		<view class="datail">
			<view class="title">{{objData.title}}</view>
			<view class="content">{{objData.body}}</view>
		</view>
		<view class="comments">
			<view class="text"></view>
			<view class="row" v-for="item in Comments" :key="item.id">
				<view class="top">
					<view class="name">{{item.name}}</view>
					<view class="mail">{{item.email}}</view>
				</view>
				<view class="body">
					{{item.body}}
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				objData: {},
				id: 1,
				Comments: [],
			};
		},
		onLoad(e) {
			console.log(e);
			this.id = e.id
			this.getDetail();
			this.getComments();
		},
		methods: {
			getDetail() {
				uni.showLoading({
						title: "数据加载中",
						mask: true
					}),
					uni.request({
						url: "http://jsonplaceholder.typicode.com/posts/" + this.id,
						success: res => {
							console.log(res);
							this.objData = res.data
						},
						complete() {
							uni.hideLoading()
						}
					})
			},
			getComments() {
				uni.request({
					url: `http://jsonplaceholder.typicode.com/posts/${this.id}/comments`,
					success: res => {
						console.log(res);
						this.Comments = res.data
					}
				})
			}
		}
	}
</script>

<style lang="scss" scoped>

</style>