<template>
	<view>
		
		<view class="bg-white overflow-h my-3 mx-3">
			<view class="px-3 py-3 border-bottom d-flex j-sb a-center font-24 color6" @click="Router.navigateTo({route:{path:'/pages/zitiAddress/zitiAddress'}})">
				<view>自提门店</view>
				<view class="arrowR"><image src="../../static/images/about-icon4.png" mode=""></image></view>
			</view>
			<view class="px-3 py-3" v-if="shopData.name" @click="Router.navigateTo({route:{path:'/pages/zitiAddress/zitiAddress'}})">
				<view class="d-flex j-sb a-center mt-1">
					<view class="mr-3 font-30">{{shopData.name}}</view>
					<view class="font-26">{{shopData.phone}}</view>
				</view>
				<view class="mt-1">{{shopData.address}}</view>
			</view>
			<view class="px-3 py-3" v-else @click="Router.navigateTo({route:{path:'/pages/zitiAddress/zitiAddress'}})">
				<!-- <view class="d-flex j-sb a-center mt-1">
					<view class="mr-3 font-30">门店名称门店名称</view>
					<view class="font-26">15689562352</view>
				</view> -->
				<view class="mt-1">请选择自提门店</view>
			</view>
			<!-- <view style="width: 100%;height: 8rpx;"><image src="../../static/images/the-orderl-img.png" mode=""></image></view> -->
		</view>
		<view class="bg-white overflow-h mx-3">
			<view class="px-3 py-3 border-bottom font-24 color6">收货人信息</view>
			<view class="px-3">
				<view class="py-3 d-flex j-sb a-center border-bottom" style="text-align: right;">
					<view>昵称</view>
					<view class="font-26 color6" style="width: 60%;">
						<open-data type="userNickName"></open-data>
					</view>
				</view>
				<view class="py-3 d-flex j-sb a-center">
					<view>电话</view>
					<view class="font-26 color6" style="width: 60%;">
						<input type="number" maxlength="11" v-model="submitData.phone" placeholder="请输入联系电话" placeholder-class=""/>
					</view>
				</view>
			</view>
		</view>
		
		<view class="proRow mt-3 mx-3">
			<view class="item d-flex j-sb mb-3" v-for="(item,index) in mainData" :key="index">
				<view class="pic">
					<image :src="item.product&&item.product.mainImg&&item.product.mainImg[0]?item.product.mainImg[0].url:''" mode=""></image>
					<view class="imgTit text-white font-22 text-center avoidOverflow px-1">本商品由生灵商行专供</view>
				</view>
				<view class="infor">
					<view class="tit avoidOverflow">{{item.product?item.product.title:''}}</view>
					<view class="d-flex font-24 color6 mt-1">
						<view class="specsBtn mr-1">{{item.product&&item.product.sku&&item.product.sku[item.skuIndex]?item.product.sku[item.skuIndex].title:''}}</view>
					</view>
					<view class="d-flex j-sb B-price">
						<view class="price font-32 font-weight">{{item.product&&item.product.sku&&item.product.sku[item.skuIndex]?item.product.sku[item.skuIndex].price:''}}</view>
						<view class="flexEnd">
							<view class="numBox d-flex">
								<view class="btn" @click="counter(index,'-')">-</view>
								<view class="num">{{item.count}}</view>
								<view class="btn pubBj white add"  @click="counter(index,'+')">+</view>
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		
		<view class="xqbotomBar pl-3">
			<view class="d-flex a-center mr-3 font-26">总计<view class="price font-weight font-30">{{totalPrice}}</view></view>
			<view class="payBtn main-bg-color text-white" style="width: 260rpx;" @click="zitiMsgShow">立即支付</view>
		</view>
		
		<!-- 优惠券 -->
		<view class="black-bj" v-show="is_show"></view>
		<view class="zitiMsgShow text-center whiteBj radius10 px-3 pt-4" v-show="is_zitiMsgShow">
			<view class="red">此商品需要您到店自提，请仔细确认地址！</view>
			<view class="f5bj px-3 py-3 mt-3 rounded10">
				<view>自提门店：{{shopData.name}}</view>
				<view class="font-26 color6 mt-1">地址：{{shopData.address}}</view>
			</view>
			<view class="pt-1 d-flex j-center a-center mt-4 font-30">
				<view class="TwoBtn border" @click="zitiMsgShow">取消付款</view>
				<button class="TwoBtn on  main-text-color ml-4" style="margin: 0;margin-left: 40rpx;background-color: #fff;font-size:15px" 
				open-type="getUserInfo"  @getuserinfo="Utils.stopMultiClick(submit)">确认付款</button>
			</view>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				Utils:this.$Utils,
				showView: false,
				score:'',
				wx_info:{},
				is_show:false,
				curr:1,
				count:1,
			
				is_zitiMsgShow:false,
				couponData:3,
				couponCurr:0,
				shopData:{},
				submitData:{
					shop_no:'',
					passage1:'',
					name:'',
					phone:''
				},
				mainData:[],
				totalPrice:0,
				pay:{}
			}
		},
		
		onLoad(options) {
			const self = this;
			self.mainData = uni.getStorageSync('payPro');
			self.submitData.name = uni.getStorageSync('user_info').nickname;
			self.countTotalPrice()
		},
		
		onShow() {
			const self = this;
			
			if(uni.getStorageSync('choosedShopData')){
				self.shopData = uni.getStorageSync('choosedShopData')
			}else{
				self.getDefalutShop()
			};
			
		},
		
		methods: {
			
			getDefalutShop() {
				const self = this;		
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				
				postData.getAfter = {
					shop:{
						tableName:'UserInfo',
						middleKey:'shop',
						key:'user_no',
						searchItem:{
							status:1
						},
						condition:'='
					}
				}
				const callback = (res) => {
					if (res.info.data.length > 0) {
						if(res.info.data[0].shop[0]){
							self.shopData= res.info.data[0].shop[0]
							self.submitData.phone = res.info.data[0].phone
							self.submitData.shop_no = self.shopData.phone
						}
					}
				};
				self.$apis.userInfoGet(postData, callback);
			},
			
			
			
			
			zitiMsgShow(){
				const self = this;
				if(JSON.stringify(self.shopData) == '{}'){
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请选择自提门店','none')
					return
				};
				if(self.submitData.phone==''){
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请填写收货人信息','none')
					return
				};
				self.is_show = !self.is_show;
				self.is_zitiMsgShow = !self.is_zitiMsgShow;
			},
			
			counter(index, type) {
				const self = this;
				if (type == '+') {
					self.mainData[index].count++;
				} else {
					if (self.mainData[index].count > 1) {
						self.mainData[index].count--;
					}
				};
				self.countTotalPrice();
			},
			
			countTotalPrice() {
				const self = this;
				self.totalPrice = 0;
				for (var i = 0; i < self.mainData.length; i++) {
					self.totalPrice += self.mainData[i].product.sku[self.mainData[i].skuIndex].price*self.mainData[i].count
				}
				
				self.totalPrice = parseFloat(self.totalPrice).toFixed(2)
				//console.log('wxPay',wxPay)
				if (self.totalPrice > 0) {
					self.pay.wxPay = {
						price: self.totalPrice,
					};
				} else {
					  delete self.pay.wxPay;	 
				};
				console.log(self.pay)
			},
			
			submit(){
				const self = this;
				uni.setStorageSync('canClick', false);
				self.is_zitiMsgShow = false;
				self.is_show = false;
				if(JSON.stringify(self.shopData) == '{}'){
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请选择自提门店','none')
					return
				}
				var data = {
					snap_address:self.shopData,
					shop_no:self.shopData.user_no
				};
				var orderList = []
				for (var i = 0; i < self.mainData.length; i++) {
					orderList.push({sku_id:self.mainData[i].sku_id,count:self.mainData[i].count,data: data,
					snap_address: self.addressData})
				}
				const callback = (user, res) => {
					if(self.submitData.name){
						self.submitData.name = user.nickName;
					}
					self.addOrder(orderList)
				};
				self.$Utils.getAuthSetting(callback);
			},
			
			addOrder(orderList) {
				const self = this;	
				
				/* if(self.orderId){
					self.goPay()
					return
				}; */
				const postData = {}; 
				postData.orderList = self.$Utils.cloneForm(orderList);
				postData.type=1;
				postData.data = {
					level:1,
					snap_address:self.addressData,
					passage1:'次日'+uni.getStorageSync('user_info').thirdApp.pickup_start+'点-'+uni.getStorageSync('user_info').thirdApp.pickup_end+'点',
					name:self.submitData.name,
					phone:self.submitData.phone,
					shop_no:self.shopData.user_no
				};
				postData.parent = 1;
				postData.tokenFuncName = 'getProjectToken';
				postData.refreshToken = true;
				const callback = (res) => {
					uni.setStorageSync('canClick', true);
					if (res && res.solely_code == 100000) {
						self.orderId = res.info.id;
						var array = self.$Utils.getStorageArray('cartData');
						for (var i = 0; i < orderList.length; i++) {
							for (var j = 0; j < array.length; j++) {
								if(orderList[i].sku_id == array[j].sku[array[j].skuIndex].id){
									self.$Utils.delStorageArray('cartData', array[j], 'id');
								}
							}
						};
						self.goPay()
					} else {		
						uni.showToast({
							title: res.msg,
							duration: 2000
						});
					};		
				};
				self.$apis.addOrder(postData, callback);
			},
			
			goPay() {
				const self = this;	
				const postData = self.$Utils.cloneForm(self.pay);	
				postData.tokenFuncName = 'getProjectToken',
				postData.searchItem = {
					id: self.orderId
				};
				postData.payAfter = [
					{
						tableName: 'UserInfo',
						FuncName: 'update',
						searchItem:{
							user_no:uni.getStorageSync('user_info').user_no
						},
						data: {
							phone:self.submitData.phone
						},
					},
				];
				const callback = (res) => {
					if (res.solely_code == 100000) {
						uni.setStorageSync('canClick', true);
					
						if (res.info) {
							const payCallback = (payData) => {
								console.log('payData', payData)
								if (payData == 1) {
									uni.showToast({
										title: '支付成功',
										duration: 1000,
										success: function() {
											
										}
									});
									setTimeout(function() {
										self.$Router.redirectTo({route:{path:'/pages/orderPayOk/orderPayOk?id='+self.orderId}})
									}, 1000);
								} else {
									uni.setStorageSync('canClick', true);
									uni.showToast({
										title: '支付失败',
										duration: 2000
									});
								};
							};
							self.$Utils.realPay(res.info, payCallback);
						} else {
							
							uni.showToast({
								title: '支付成功',
								duration: 1000,
								success: function() {
									
								}
							});
							setTimeout(function() {
								self.$Router.redirectTo({route:{path:'/pages/orderPayOk/orderPayOk?id='+self.orderId}})
							}, 1000);
						};
					} else {
						uni.setStorageSync('canClick', true);
						uni.showToast({
							title: res.msg,
							duration: 2000
						});
					};
				};
				self.$apis.pay(postData, callback);
			},
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
