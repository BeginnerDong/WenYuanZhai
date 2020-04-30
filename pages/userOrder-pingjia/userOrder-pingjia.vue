<template>
	<view>
		
		<view class="mx-3">
			<view class="proRow">
				<view class="item my-3">
					<view class="font-24 d-flex j-sb a-center pb-2 border-bottom">
						<view class="color9">订单编号:152565622323</view>
						<view class="red">已提货</view>
					</view>
					<view class="d-flex j-sb a-center py-2 inforLine">
						<view class="picBox d-flex a-center flex-wrap">
							<image src="../../static/images/shopping-img.png" mode=""></image>
							<image src="../../static/images/shopping-img.png" mode=""></image>
							<image src="../../static/images/shopping-img.png" mode=""></image>
						</view>
						<view class="rr d-flex j-end a-center">
							<image class="arrowR" src="../../static/images/about-icon4.png" mode=""></image>
						</view>
					</view>
					<view class=" d-flex j-sb a-center pt-3 border-top">
						<view class="font-24 color9">2020.04.30 10:02</view>
						<view class="font-26">共3件商品 合计:<span class="price">56</span></view>
					</view>
				</view>
			</view>
			
			<view class="bg-white rounded10 px-3 py-3">
				<view class="font-26">
					<textarea value="" placeholder="请填写商品评论,让更多人知道" />
				</view>
				<view class="d-flex a-center">
					<view class="d-flex a-center flex-wrap onloadbtn">
						<image src="../../static/images/commentsl-icon.png" mode=""></image>
					</view>
					<view class="font-24 color9 ml-2">可上传多张照片</view>
				</view>
				<view class="d-flex a-start flex-wrap pjPic">
					<image src="../../static/images/shopping-img.png" mode=""></image>
					<image src="../../static/images/shopping-img.png" mode=""></image>
					<image src="../../static/images/shopping-img.png" mode=""></image>
				</view>
				
			</view>
		</view>
		
		<view class="submitbtn" style="margin-top: 120rpx;">
			<button class="btn" type="button" @click="Router.navigateTo({route:{path:'/pages/userOrder/userOrder'}})">确定</button>
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
				wx_info:{}
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
	@import "../../assets/style/proRow.css";
	page{background: #F5F5F5;padding-bottom: 60rpx;}
	textarea{font-size: 26rpx;width: 100%;height:240rpx;padding: 0;}
	.onloadbtn{width: 120rpx;height: 120rpx;}
	.pjPic image{width: 142rpx;height: 142rpx;margin: 20rpx 20rpx 0 0;border-radius: 10rpx;}
	.pjPic image:nth-of-type(4n){margin-right: 0;}
</style>
