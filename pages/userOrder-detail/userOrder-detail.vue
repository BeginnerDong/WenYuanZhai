<template>
	<view>
		<view class="mx-3 mt-3">
			
			<view class="HeadState rounded10 bg-white">
				<view style="width: 100%;height: 8rpx;"><image src="../../static/images/the-orderl-icon2.png" mode=""></image></view>
				<view class="infor px-3 py-3 d-flex j-center a-center" style="height: 136rpx;">
					<view class="d-flex j-sb a-center w-100">
						<view class="d-flex a-center main-text-color font-28" v-if="mainData.transport_status==0&&mainData.pay_status==1">
							<image style="width: 30rpx; height: 27rpx;margin-right: 10rpx;" src="../../static/images/the-orderl-icon.png" 
							mode=""></image>待提货
						</view>
						<view class="d-flex a-center main-text-color font-28" v-if="mainData.transport_status==1&&mainData.pay_status==1">
							<image style="width: 30rpx; height: 27rpx;margin-right: 10rpx;" src="../../static/images/the-orderl-icon.png" 
							mode=""></image>已提货
						</view>
						<view class="d-flex a-center main-text-color font-28" v-if="mainData.pay_status==0">
							<image style="width: 30rpx; height: 27rpx;margin-right: 10rpx;" src="../../static/images/the-orderl-icon.png" 
							mode=""></image>未付款
						</view>
						<view class="d-flex j-end a-center font-26" v-if="mainData.transport_status==0&&mainData.pay_status==1">
							<view class="d-block a-center">提货单号：<span class="main-text-color">{{mainData.id}}</span></view>
							<view class="ml-3"><image class="samllEwm" @click="previewImg(0)" :src="mainData.qrcode" mode=""></image></view>
						</view>
					</view>
				</view>
			</view>
			
			<view class="bg-white rounded10 px-3 py-3 mt-3 font-26">
				<view>收货人：{{mainData.name?mainData.name:''}} {{mainData.phone?mainData.phone:''}}</view>
				<view class="my-2 main-text-color">自提点：{{mainData.shop&&mainData.shop.name?mainData.shop.name:''}}</view>
				<view class="color6">地址：{{mainData.shop&&mainData.shop.address?mainData.shop.address:''}}</view>
			</view>
			
			<view class="proRow mt-3">
				<view class="item mb-2 rounded10" >
					<view class="mb-3" v-for="(item,index) in mainData.child" :key="index">
						<view class="d-flex j-sb a-center">
							<view class="pic">
								<image :src="item.orderItem&&item.orderItem[0]&&item.orderItem[0].snap_product&&item.orderItem[0].snap_product.product&&
								item.orderItem[0].snap_product.product.mainImg&&item.orderItem[0].snap_product.product.mainImg[0]?item.orderItem[0].snap_product.product.mainImg[0].url:''" mode=""></image>
								<view class="imgTit text-white font-22 text-center avoidOverflow px-1">本商品由生灵商行专供</view>
							</view>
							<view class="infor">
								<view class="avoidOverflow font-28">{{item.orderItem&&item.orderItem[0]&&item.orderItem[0].snap_product&&item.orderItem[0].snap_product.product?item.orderItem[0].snap_product.product.title:''}}</view>
								<view class="d-flex font-24 color6 mt-1">
									<view class="specsBtn mr-1">{{item.orderItem&&item.orderItem[0]&&item.orderItem[0].snap_product&&item.orderItem[0].snap_product?item.orderItem[0].snap_product.title:''}}</view>
								</view>
								<view class="B-price">
									<view class=""></view>
									<view class=" d-flex j-sb a-center">
										<view class="price font-26">{{item.unit_price}}</view>
										<view class="font-26">×{{item.count}}</view>
									</view>
								</view>
							</view>
						</view>
					</view>
					<view class="mt-3 font-26 d-flex j-end a-center">共{{mainData.child?mainData.child.length:''}}件商品 实付金额:<span class="price font-30 font-weight">{{mainData.price}}</span></view>
				</view>
			</view>	
		
			<view class="bg-white rounded10 px-3 py-3 mt-3 font-26 color6">
				<view class="mb-2">订单编号：{{mainData.order_no?mainData.order_no:''}}</view>
				<view>下单时间：{{mainData.create_time?mainData.create_time:''}}</view>
			</view>
			
			<view class="px-3 text-center FixB-btn main-bg-color text-white" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">继续购物</view>
		</view>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router: this.$Router,
				mainData: {}
			}
		},	
		
		onLoad(options) {
			const self = this;
			self.id = options.id;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			previewImg() {
				const self = this;
				var urls = [self.mainData.qrcode]
				uni.previewImage({
					urls: urls,
					longPressActions: {
						itemList: ['发送给朋友', '保存图片', '收藏'],
						success: function(data) {
							
						},
						fail: function(err) {
							console.log(err.errMsg);
						}
					}
				});
			},
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					id: self.id,
				};
				postData.getAfter = {
					shop: {
						tableName: 'UserInfo',
						middleKey: 'shop_no',
						key: 'user_no',
						searchItem: {
							status: 1,
							user_type: 1
						},
						condition: '=',
						info: ['name', 'address']
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
					};
					console.log('self.mainData', self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.orderGet(postData, callback);
			},
		}
	};
</script>

<style>
	@import "../../assets/style/proRow.css";
	
	page{background: #F5F5F5;padding-bottom: 120rpx;}
	
	
	.proRow .item .infor{width: 72%;}
	
	.samllEwm{width: 78rpx;height: 78rpx;}
	
	.FixB-btn{position: fixed;left: 0;right: 0;bottom: 0;height: 80rpx;line-height: 80rpx;}
</style>
