<template>
	<view>
		<view class="">
			<ul v-for="item in lianxi" :key="item.id">
				<li>{{item.value}}</li>
			</ul>
			<view class="" @click="postrequset()">Hello</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				lianxi: [{
						value: '维修服务',
						id: 1
					},
					{
						value: '应用bug',
						id: 2
					},
					{
						value: '',
						id: 3
					},
					{
						value: '',
						id: 4
					},
					{
						value: '',
						id: 5
					},
				]
			};
		},
		methods: {
			postrequset() {
				uni.request({
					url: "192.168.12.32:8080/sys/login",
					data: {
						"username": "zs",
						"password": "123456",
					},
					method: "POST",
					header: {
						"Content-Type": "application/x-www-form-urlencoded"
					},
					success: res => {
						console.log(1);
						console.log(res.data);
						console.log(2);
						console.log(res.code);
						console.log(3);
						console.log(res.msg);
					},
					fail() {

						uni.showModal({
							title: "请检查网络设置"
						})
					},
				})
			}
		}
	}
</script>

<style lang="scss">

</style>