<template>
	<view>
		<view class="headTit text-center position-relative text-white">
			<image src="../../static/images/pay-for-successl-img.png" mode=""></image>
			<view class="tit font-36">您的提货单号：9</view>
		</view>
		
		<view class="px-3 okCont">
			<view class="okIcon"><image src="../../static/images/pay-for-successl-icon.png" mode=""></image></view>
			<view class="text-center mb-5">支付成功</view>
			
			<view class="seltBtn d-flex j-sb a-center font-28  text-center color2 pt-2" style="width:85%;margin:0 auto ;">
				<view class="btn color6" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">继续购物</view>
				<view class="btn on" @click="Router.navigateTo({route:{path:'/pages/share-detail/share-detail'}})">提醒老板接单</view>
			</view>
			<view class="font-24 mt-4 color6" style="line-height: 40rpx;">点击上面的<span class="font-weight  main-text-color">“提醒老板接单”</span>按钮，将提醒消息发送到该店客户微信群：<span class="red">“文远斋001”</span>群，提醒老板及时处理您的订单</view>
			
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				showView: false,
				score:'',
				wx_info:{},
				is_show:false
			}
		},
		onLoad() {
			const self = this;
			//self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			
		}
	};
</script>

<style>
	page{padding-bottom: 60rpx;}
	.headTit image{width: 100%;height: 270rpx;}
	.headTit .tit{position: absolute;top: 100rpx;left: 4%;right: 4%;z-index: 1;}
	.okIcon{width: 231rpx;height: 220rpx;margin: 60rpx auto 40rpx auto;}
	.okIcon image{width: 100%;height: 100%;}
	
	.seltBtn .btn{width: 260rpx;height: 70rpx;line-height: 70rpx;border-radius:40rpx;border:1px solid #ccc;}
	.seltBtn .btn.on{border-color: #E1211C;color: #E1211C;}
	
</style>
