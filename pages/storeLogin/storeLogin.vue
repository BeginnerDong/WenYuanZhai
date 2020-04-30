<template>
	<view>
		
		<view class="loginBj position-relative text-white">
			<view class="topTitle mt-5" style="font-size: 16px;height: 40px; line-height: 40px;">
				<view class="backBtn ml-2" @click="navigateBack"><image src="../../static/images/back-Wicon.png" mode=""></image></view>
				<view class="text-center">登录</view>
			</view>
			<view class="bj"><image src="../../static/images/the-loginl-img.png" mode=""></image></view>
		</view>
		
		<view class="loginCont">
			<view class="item d-flex a-center border-bottom">
				<view class="icon"><image src="../../static/images/the-loginl-icon.png" mode=""></image></view>
				<view class="input">
					<input type="text" value="" placeholder="请输入账号" placeholder-class="placeholder">
				</view>
			</view>
			<view class="item d-flex a-center mt-4 border-bottom">
				<view class="icon"><image src="../../static/images/the-loginl-icon1.png" mode=""></image></view>
				<view class="input">
					<input type="password" value="" placeholder="请输入密码" placeholder-class="placeholder">
				</view>
			</view>
			
			<view class="item submitbtn" style="padding: 0;border: 0;margin-top: 100rpx;" @click="Router.navigateTo({route:{path:'/pages/storeOrder/storeOrder'}})">
				<button class="Wbtn" type="submint">登录</button>
			</view>
		</view>
		
		
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				is_show: false,
				wx_info:{}
			}
		},
		onLoad() {
			const self = this;
			
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			navigateBack(){
				uni.navigateBack()
			},
			getMainData() {
				const self = this;
				console.log('852369')
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				self.$apis.orderGet(postData, callback);
			}
		}
	};
</script>

<style>
	
	page{padding-bottom: 60rpx;}	
	.loginBj{width: 100%;height: 450rpx;}
	.loginBj .bj{width: 100%;height: 100%;}
	.topTitle{position: absolute;left: 0;top: 0;right: 0; z-index: 1;}
	.backBtn{width:20rpx;height: 35rpx;position: absolute;top: 24rpx;left: 20rpx; z-index: 1;}
	
	.loginCont{width:90%;margin: 0 auto;z-index: 2;background: #fff;padding: 0rpx 60rpx;box-sizing: border-box;padding-top: 100rpx;}
	.loginCont .item{height: 80rpx;}
	.loginCont .item .icon{width: 36rpx;height: 36rpx;margin-right: 30rpx;}
	.loginCont .item .input{width: 85%;}
	.loginCont .item .input input{font-size: 26rpx;height: 60rpx;}
</style>
