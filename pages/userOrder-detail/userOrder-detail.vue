<template>
	<view>
		<view class="mx-3 mt-3">
			
			<view class="HeadState rounded10 bg-white">
				<view style="width: 100%;height: 8rpx;"><image src="../../static/images/the-orderl-icon2.png" mode=""></image></view>
				<view class="infor px-3 py-3 d-flex j-center a-center" style="height: 136rpx;">
					<view class="d-flex j-sb a-center w-100">
						<view class="d-flex a-center main-text-color font-28"><image style="width: 30rpx; height: 27rpx;margin-right: 10rpx;" src="../../static/images/the-orderl-icon.png" mode=""></image>待提货</view>
						<view class="d-flex j-end a-center font-26">
							<view class="d-block a-center">提货单号：<span class="main-text-color">8</span></view>
							<view class="ml-3"><image class="samllEwm" src="../../static/images/the-orderl-img.png" mode=""></image></view>
						</view>
					</view>
				</view>
			</view>
			
			<view class="bg-white rounded10 px-3 py-3 mt-3 font-26">
				<view>收货人：张丹 15623565689</view>
				<view class="my-2 main-text-color">自提点：门店名称门店名称</view>
				<view class="color6">地址：陕西省西安市高新区高新大都会A座</view>
			</view>
			
			<view class="proRow mt-3">
				<view class="item mb-2 rounded10" >
					<view class="mb-3" v-for="(item,index) in mainData" :key="index">
						<view class="d-flex j-sb a-center">
							<view class="pic">
								<image src="../../static/images/shopping-img.png" mode=""></image>
								<view class="imgTit text-white font-22 text-center avoidOverflow px-1">本商品由生灵商行专供</view>
							</view>
							<view class="infor">
								<view class="avoidOverflow font-28">智利车厘子 约200g/份 正负20g</view>
								<view class="d-flex font-24 color6 mt-1">
									<view class="specsBtn mr-1">大份</view>
								</view>
								<view class="B-price">
									<view class=""></view>
									<view class=" d-flex j-sb a-center">
										<view class="price font-26">18.8</view>
										<view class="font-26">×1</view>
									</view>
								</view>
							</view>
						</view>
					</view>
					<view class="mt-3 font-26 d-flex j-end a-center">共1件商品 实付金额:<span class="price font-30 font-weight">56</span></view>
				</view>
			</view>	
		
			<view class="bg-white rounded10 px-3 py-3 mt-3 font-26 color6">
				<view class="mb-2">订单编号：5522256553326567</view>
				<view>下单时间：2020-03-05 17:20:40</view>
			</view>
			
			<view class="px-3 text-center FixB-btn main-bg-color text-white" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">继续购物</view>
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
				mainData:[{},{},{}],
				is_popupShow:false,
			}
		},
		onLoad() {
			const self = this;
			//self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			popupShow(){
				const self=this;
				self.is_popupShow = !self.is_popupShow;
				self.is_show = !self.is_show;
				
			}
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
