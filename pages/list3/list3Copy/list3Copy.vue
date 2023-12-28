<template>
	<view class="mainList3" :style="">
		<view style="margin-top: 64rpx;" v-show="yemian>0"></view>
		<view class="" v-show="yemian>=1" @click="yemianchange0()"><返回</view>
		<view class="fuwu" v-show="yemian === 2">
			<view class="shuru">
				<input type="text" placeholder="点击发送消息"><button size="mini">发送</button>
			</view>
		</view>
		<view class="lianxiwomen" v-show="yemian === 3">
			<ul>
				<li class="topli">邮箱：</li>
				<li>www.baidu.com</li>
				<li class="topli">微信：</li>
				<li>weixin</li>
				<li class="topli">电话</li>
				<li>10086</li>
			</ul>
		</view>
	<view class="wo" v-show="yemian===0">
		<view class="userimfo">
			<view class="userlogo">
				<image src="../../../static/userlogo.png" mode=""></image>
			</view>
			<view class="nihao">
				你好！
			</view>
			<view class="nihaouser">
				{{use_name}}
			</view>
		</view>
		<view class="use-info">
			<ul>
				<li class="firstLi" @click="toUesrInformation()"><view class="viewim"><image src="../../../static/userimfo.png"></image></view>用户信息<view class="enter">></view></li>
				<li class="secondLi" @click="tofuwu()"><view class="viewim"><image src="../../../static/server.png"></image></view>服务<view class="enter">></view></li>
				<li @click="yemian=3"><view class="viewim"><image src="../../../static/futianquan12.jpg"></image></view>联系我们<view class="enter">></view></li>
				<li class="lastLi" @click="tosheshi()"><view class="viewim"><image src="../../../static/setting.png"></image></view>版本信息<view class="enter">></view></li>
			</ul>
			<view class="comabackdenglu">
				<button class="comabackdenglubut" plain="true" type="default" size="mini" @click="comebackdenglu">{{fanhui}}</button>
			</view>
		</view>
	</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				fanhui:'返回登陆',
				use_name:'',
				use_info1:'',
				use_info2:'',
				yemian:0,
				userinformation :[
						{id:'001',name:'名称',info:'admin'},
						{id:'002',name:'呢称',info:'Dantes'},
						{id:'003',name:'电话',info:'10086'},
						{id:'004',name:'地点',info:'NIT'},
					],
					e:0
			}
		},
		onShow() {
		},
		onLoad() {
			let that = this
			uni.getStorage({
				key:'admin',
				success(res) {
					that.use_name = res.data
				},
				fail() {
					console.log('用户名获取失败');
				}
			})
			uni.getStorage({
				key:'paassword',
				success(res) {
					that.use_info1 = res.data
				}
			})
		},
		methods: {
			toUesrInformation(){
				uni.navigateTo({
					url:"/pages/list3/userInformation/userInformation",
					success() {
						console.log("跳转至用户信息界面");
					}
				})
			},
			tosheshi(){
				uni.navigateTo({
					url:'/pages/shezhi/shezhi'
				})
			},
			tofuwu(){
				uni.navigateTo({
					url:"/pages/list3/list3Copy/list3Copy",
				})
			},
			comebackdenglu(){
				uni.navigateTo({
					url: '../login/login',
					success() {
						console.log("返回登录");
					}
				});
			},
			xiugai(){
			},
			yemianchange0(){
				this.yemian = 0
				var e= uni.getStorageSync("shezhi")
				if(e === 2){
					uni.switchTab({
						url:'/pages/list1/list1',
					})
				}
			}
		},
		components:{
		}
	}
</script>

<style lang="scss" scoped>
	.mainList3{
		height: 100vh;
		width: 100vw;
		background-color: #273333;
		box-sizing: border-box;
		padding: 0;
		margin: 0;
		.shezhi{
			margin-top: 20vh;
			.version-updating{
				
			}
		}
		.lianxiwomen{
			ul{
				margin-top: 10vh;
				li{
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
				.topli{
				    border: 0rpx;
					user-select: none;
					color: #989cab;
				}
			}
		}
		.userimfo{
			height: 24vh;
			width: 100vw;
			background-color: white;
		    .userlogo{
				float: left;
				height: 8vh;
				width: 120rpx;
				margin-top: 100rpx;
				margin-left: 3vh;
				image{
					height: 8vh;
					width: 120rpx;
				}
		   }
		   .nihao{
			   margin-top: 8vh;
			   margin-left: 3vh;
			   float: left;
			   height: 6vh;
			   width: 120rpx;
			   line-height: 3vh;
		   }
		   .nihaouser{
			   margin-top: 12vh;
			   float: left;
			   font-style: italic;
			   font-size: 3vh;
			   margin-left: -10vh;
			   height: 6vh;
			   width: 120rpx;
		   }
		}
		.use-info{
			margin: 1vh auto;
			justify-content: space-between;
			ul{
				height: 80vh;
				font-size: 36rpx;
				.firstLi{
					margin-bottom: 2vh;
				}
				.secondLi{
					border-bottom: transparent solid 1rpx;
				}
				.lastLi{
					margin-top: 2vh;
				}
				li{
					display: block;
					width: 100%;
					height: 8vh;
					line-height: 8vh;
					border-radius: 1vh;
					background-color: white;
					border: #a0cfff solid 1rpx;
					.viewim{
						float: left;
						width: 40px;
						image{
							width: 3vh;
							height: 3vh;
						}
					}
					.enter{
						float: right;
						height: 100%;
					}
				}
			}
			.comabackdenglu{
				margin: -36vh auto;
				height: 6vh;
				width: 400rpx;
				text-align: center;
				.comabackdenglubut{
					width: 360rpx;
					margin: 0rpx auto;
				}
			}
		}
	}
</style>
