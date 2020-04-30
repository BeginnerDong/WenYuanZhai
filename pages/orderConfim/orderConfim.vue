<template>
	<view>
		
		<view class="bg-white overflow-h my-3 mx-3">
			<view class="px-3 py-3 border-bottom d-flex j-sb a-center font-24 color6" @click="Router.navigateTo({route:{path:'/pages/zitiAddress/zitiAddress'}})">
				<view>自提门店</view>
				<view class="arrowR"><image src="../../static/images/about-icon4.png" mode=""></image></view>
			</view>
			<view class="px-3 py-3" @click="Router.navigateTo({route:{path:'/pages/zitiAddress/zitiAddress'}})">
				<view class="d-flex j-sb a-center mt-1">
					<view class="mr-3 font-30">门店名称门店名称</view>
					<view class="font-26">15689562352</view>
				</view>
				<view class="mt-1">陕西省西安市雁塔区高新大都荟</view>
			</view>
			<!-- <view style="width: 100%;height: 8rpx;"><image src="../../static/images/the-orderl-img.png" mode=""></image></view> -->
		</view>
		<view class="bg-white overflow-h mx-3">
			<view class="px-3 py-3 border-bottom font-24 color6">收货人信息</view>
			<view class="px-3">
				<view class="py-3 d-flex j-sb a-center border-bottom">
					<view>昵称</view>
					<view class="font-26 color6" style="width: 60%;">
						<input type="text" value="哆啦呆萌" placeholder="" placeholder-class=""/>
					</view>
				</view>
				<view class="py-3 d-flex j-sb a-center">
					<view>电话</view>
					<view class="font-26 color6" style="width: 60%;">
						<input type="number" maxlength="11" value="15258252035" placeholder="" placeholder-class=""/>
					</view>
				</view>
			</view>
			
		</view>
		
		<view class="proRow mt-3 mx-3">
			<view class="item d-flex j-sb mb-3" >
				<view class="pic">
					<image src="../../static/images/shopping-img.png" mode=""></image>
					<view class="imgTit text-white font-22 text-center avoidOverflow px-1">本商品由生灵商行专供</view>
				</view>
				<view class="infor">
					<view class="tit avoidOverflow">墨西哥牛油果8枚单果200g左右</view>
					<view class="d-flex font-24 color6 mt-1">
						<view class="specsBtn mr-1">大份</view>
					</view>
					<view class="d-flex j-sb B-price">
						<view class="price font-32 font-weight">56</view>
						<view class="flexEnd">
							<view class="numBox d-flex">
								<view class="btn" @click="counter('-')">-</view>
								<view class="num">{{count}}</view>
								<view class="btn pubBj white add" @click="counter('+')">+</view>
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		
		
		
		<view class="xqbotomBar pl-3">
			<view class="d-flex a-center mr-3 font-26">总计<view class="price font-weight font-30">79</view></view>
			<view class="payBtn main-bg-color text-white" style="width: 260rpx;" @click="zitiMsgShow">立即支付</view>
		</view>
		
		<!-- 优惠券 -->
		<view class="black-bj" v-show="is_show"></view>
		<view class="zitiMsgShow text-center whiteBj radius10 px-3 pt-4" v-show="is_zitiMsgShow">
			<view class="red">此商品需要您到店自提，请仔细确认地址！</view>
			<view class="f5bj px-3 py-3 mt-3 rounded10">
				<view>自提门店：门店名称名称</view>
				<view class="font-26 color6 mt-1">地址：陕西省西安市高新大都会A座2007</view>
			</view>
			<view class="pt-1 d-flex j-center a-center mt-4 font-30">
				<view class="TwoBtn border" @click="zitiMsgShow">取消付款</view>
				<view class="TwoBtn on  main-text-color ml-4" @click="Router.navigateTo({route:{path:'/pages/orderPayOk/orderPayOk'}})">确认付款</view>
			</view>
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
				is_show:false,
				curr:1,
				count:1,
				is_show:false,
				is_zitiMsgShow:false,
				couponData:3,
				couponCurr:0
			}
		},
		onLoad() {
			const self = this;
			//self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			couponChange(index){
				const self = this;
				self.couponCurr = index;
			},
			zitiMsgShow(){
				const self = this;
				self.is_show = !self.is_show;
				self.is_zitiMsgShow = !self.is_zitiMsgShow;
			},
			counter(type) {
				const self = this;			
				if (type == '+') {
					self.count++;
				} else {
					if (self.count > 1) {
						self.count--;
					}
				};			
				self.countTotalPrice();
			}
		}
	};
</script>

<style>
	@import "../../assets/style/detail.css";
	@import "../../assets/style/proRow.css";
	page{background: #F5F5F5;padding-bottom: 140rpx;box-sizing: border-box;}
	
	input{width: 100%; line-height: 48rpx;height: 48rpx;display: block;box-sizing: border-box;font-size: 26rpx; color: #666;text-align: right;}
	
	.proRow .item .infor{width: 72%;}
	
	.xqbotomBar .payBtn{width: 350rpx;}
	.zitiMsgShow{width: 100%;position: fixed;left: 0;right: 0;bottom: 0;height:500rpx;z-index: 50;padding-bottom: 80rpx;border-radius: 20rpx 20rpx 0 0;}
	.seltIcon{width: 36rpx;height: 36rpx;}
	.TwoBtn{width: 260rpx;height: 80rpx;line-height: 76rpx;border-radius: 40rpx;}
	.TwoBtn.on{border: 1px solid #db1b1b;}
</style>
