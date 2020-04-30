<template>
	<view>
		
		<view class="topNavFix f5bj">
			<view class="orderNav bg-white d-flex j-sb a-center shadow color6">
				<view class="tt" :class="curr==1?'on':''" @click="changeCurr('1')">全部</view>
				<view class="tt" :class="curr==2?'on':''" @click="changeCurr('2')">待核销</view>
				<view class="tt" :class="curr==3?'on':''" @click="changeCurr('3')">已核销</view>
			</view>
		</view>
		<view class="topNavH"></view>
		
		<view class="mt-3 mx-3">
			<view class="proRow">
				<view class="item mb-3">
					<view class="font-24 d-flex j-sb a-center pb-2 border-bottom">
						<view class="color9">订单编号:152565622323</view>
						<view class="red" v-if="curr==1||curr==2">待核销</view>
						<view class="red" v-if="curr==3">已核销</view>
					</view>
					<view class="d-flex j-sb a-center py-2 inforLine" @click="Router.navigateTo({route:{path:'/pages/storeOrder-detail/storeOrder-detail'}})">
						<view class="picBox d-flex a-center flex-wrap">
							<image src="../../static/images/shopping-img.png" mode=""></image>
							<image src="../../static/images/shopping-img.png" mode=""></image>
							<image src="../../static/images/shopping-img.png" mode=""></image>
						</view>
						<view class="rr d-flex j-end a-center">
							<image class="arrowR" src="../../static/images/about-icon4.png" mode=""></image>
						</view>
					</view>
					<view class=" d-flex j-sb a-center py-3 border-top">
						<view class="font-24 color9">2020.04.30 10:02</view>
						<view>共3件商品 合计:<span class="price">56</span></view>
					</view>
					<view class="underBtn d-flex j-sb a-center py-3 border-top font-26">
						<view>提货单号：<span class="red">3</span></view>
					</view>
				</view>
			</view>
		</view>
		
		<view class="R-fixIcon"><image src="../../static/images/merchantsl-icon.png" mode="" @click="Router.navigateTo({route:{path:'/pages/storeOrder-detail/storeOrder-detail'}})"></image></view>
		
		<!-- 无数据 -->
		<view class="nodata"><image src="../../static/images/nodata.png" mode=""></image></view>
		
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
				is_show:false,
				curr:1
				// orderData:2
			}
		},
		onLoad() {
			const self = this;
			//self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			changeCurr(curr){
				const self = this;
				if(curr!= self.curr){
					self.curr = curr
				}
			}
		}
	};
</script>

<style>
	@import "../../assets/style/orderNav.css";
	@import "../../assets/style/proRow.css";
	page{background: #F5F5F5;}
	
	.topNavFix{width: 100%;height: 80rpx;position: fixed;top:0rpx;right: 0;left: 0;box-sizing: border-box;z-index: 22;}
	.topNavH{height: 80rpx;}
	
	.proRow .item{padding: 20rpx 30rpx 0 30rpx;}
	.orderNav .tt.on::after{bottom: 0;}
	
	
</style>
