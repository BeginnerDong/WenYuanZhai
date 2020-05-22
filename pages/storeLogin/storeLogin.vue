<template>
	<view v-if="showAll">
		
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
					<input type="text" v-model="submitData.login_name" placeholder="请输入账号" placeholder-class="placeholder">
				</view>
			</view>
			<view class="item d-flex a-center mt-4 border-bottom">
				<view class="icon"><image src="../../static/images/the-loginl-icon1.png" mode=""></image></view>
				<view class="input">
					<input type="password" v-model="submitData.password" placeholder="请输入密码" placeholder-class="placeholder">
				</view>
			</view>
			
			<view class="item submitbtn" style="padding: 0;border: 0;margin-top: 100rpx;">
				<button class="Wbtn" type="submint" @click="submit">登录</button>
			</view>
		</view>
		
		
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				submitData:{
					login_name:'',
					password:''
				},
				showAll:false
			}
		},
		onLoad() {
			const self = this;
			uni.hideLoading();
			if (uni.getStorageSync('merchant_token')) {
				uni.redirectTo({
					url: '/pages/storeOrder/storeOrder'
				})
			}else{
				self.showAll = true
			}
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			navigateBack(){
				uni.navigateBack()
			},
			submit() {
				const self = this;
				const postData = {
					login_name: self.submitData.login_name,
					password:self.submitData.password
				};
				if (self.$Utils.checkComplete(self.submitData)) {
					const callback = (res) => {
						if (res.solely_code == 100000) {
							console.log(res);
							uni.setStorageSync('merchant_token', res.token);
							uni.setStorageSync('merchant_info', res.info);
							setTimeout(function() {
								self.Router.reLaunch({route:{path:'/pages/storeOrder/storeOrder'}})
							}, 1000);
						} else {
							self.$Utils.showToast(res.msg,'none')
						}
					}
					self.$apis.shopLogin(postData, callback);
				} else {
					self.$Utils.showToast('请补全登录信息', 'none')
				};
			},
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
