<template>
	<view>
		
		<view class="homeHead position-relative">
			<view class="px-3 py-3 d-flex text-white GpsAdrs a-start">
				<view class="GpsIcon mr-1"><image src="../../static/images/home-icon.png" mode=""></image></view>
				<view>{{city}}</view>
			</view>
			<view class="banner-box px-3" style="margin-top: -160rpx;" >
				<swiper class="swiper-box rounded10 overflow-h" indicator-dots="true" autoplay="true" interval="3000" duration="1000" indicator-color="#d89c9c" indicator-active-color="#db1b1b">
					<block v-for="(item,index) in sliderData.mainImg" :key="index">
						<swiper-item class="swiper-item">
							<image :src="item.url" class="slide-image" />
						</swiper-item>
					</block>
				</swiper>
			</view>
		</view>
		
		<view class="px-3 mt-4">
			<view class="d-flex  a-center">
				<view class="title-xian mr-4 pb-2" v-for="(item,index) in labelData" :key="index"
				:class="curr==index?'on':''" @click="currChange(index)">{{item.title}}</view>
			</view>
			
			<view class="productList">
				<view class="item pb-3 mt-3 border-bottom shadow rounded10 overflow-h" v-for="(item,index) in mainData" :key="index">
					<view class="pic rounded10 overflow-h position-relative" :data-id="item.id"
				@click="Router.navigateTo({route:{path:'/pages/productDetail/productDetail?id='+$event.currentTarget.dataset.id}})">
						<view class="fixState no" style="background-color: #7d7d7d;" v-if="!canBuy">不可买</view>
						<view class="fixState"  style="background-color: #37c25b;" v-if="canBuy">可买</view>
						<image class="img" :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" mode=""></image>
						<!-- <view class="imgTit text-white font-23 text-center avoidOverflow px-3">本商品由生灵商行专供</view> -->
					</view>
					<view class="infor mt-3 px-3 d-flex j-sb a-center">
						<view>
							<view  class="d-flex mt-1 a-center">
								<view class="tit avoidOverflow2 font-30 font-weight" style="width: 90%;">{{item.title}}</view>
								
							</view>
							
							<view class="d-flex mt-1 a-center">
								<view class="price font-32 font-weight">{{item.price}}</view>
								<!-- <view style="font-size:26rpx;color:#666;margin-left: 20rpx;">库存：{{item.stock}}</view> -->
								<view style="font-size:26rpx;color:#666;margin-left: 20rpx;">销量：{{item.sale_count}}</view>
							</view>
						</view>
						
						<view style="width: 80rpx;height: 80rpx;justify-content: flex-end;display: flex;" @click="addCar(index)">
							<image src="../../static/images/home-icon9.png" mode=""></image>
						</view>
						
					</view>
				</view>
			</view>
			
			<!-- 无数据 -->
			<view class="nodata" v-if="mainData.length==0"><image src="../../static/images/nodata.png" mode=""></image></view>
			
		</view>
		
		<!--底部tab键-->
		<view class="navbar">
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<view class="nav_img">
					<image src="../../static/images/nabar1-a.png" />
				</view>
				<view class="text this-text">首页</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/car/car'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar2.png" />
				</view>
				<view class="text">购物车</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar3.png" />
				</view>
				<view class="text">我的</view>
			</view>
		</view>
		<!--底部tab键 end-->
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				curr:0,
				mainData:[],
				labelData:[],
				sliderData:{},
				city:'',
				canBuy:false
			}
		},
		onLoad() {
			const self = this;
			const callback = (res) => {
				self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
				self.$Utils.loadAll(['getUserData','getLocation','getLabelData','getSliderData'], self);
			};
			self.$Token.getProjectToken(callback, {
				refreshToken: true
			})
			
		},
		
		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},
		
		methods: {
			
			
			addCar(index){
				const self = this;
				if (!self.canBuy) {
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('商品暂不可购买', 'none');
					return
				};
				var obj = self.mainData[index];
				self.mainData[index].skuIndex = 0;
				var array = self.$Utils.getStorageArray('cartData');
				for (var i = 0; i < array.length; i++) {
					if (array[i].sku[array[i].skuIndex].id == self.mainData[index].sku[0].id) {
						var target = array[i]
					}
				}
				if (target) {
					target.count = target.count + 1
				} else {
					var target = self.mainData[index];
					target.count = 1;
					target.isSelect = true;
				}
				self.$Utils.showToast('加入成功', 'none');
				self.$Utils.setStorageArray('cartData', target, 'id', 999);
			},
			
			getUserData() {
				var self = this;
				var postData = {};
				postData.tokenFuncName = 'getProjectToken';
				var callback = function(res) {
					if (res.info.data.length > 0 && res.info.data[0]) {
						self.userData = res.info.data[0]
						var d = new Date();
						var h = d.getHours();
						if(h>uni.getStorageSync('user_info').thirdApp.start_time&&h<uni.getStorageSync('user_info').thirdApp.end_time){
							self.canBuy = true
						}
					};
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},
			
			getLocation() {
				const self = this;
				const callback = (res) => {
					if (res) {
						console.log('res', res)
						/* if(res.authSetting){
							self.data.is_show=true;
							self.setData({
								is_show:self.data.is_show
							})
							return
						} */
						self.city = res.formatted_addresses.recommend
					};
					self.$Utils.finishFunc('getLocation');
				};
				self.$Utils.getLocation('reverseGeocoder', callback);
			},
			
			currChange(curr){
				const self = this;
				if(curr!=self.curr){
					self.curr = curr;
					self.currentId = self.labelData[self.curr].id;
					self.getMainData(true)
				}
			},
			
			getMainData(isNew) {
				var self = this;
				if (isNew) {
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage: 1,
						pagesize: 10,
						is_page: true,
					}
				};
				var postData = {};
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = {
					thirdapp_id: 2,
					type:1,
					category_id:self.currentId
				};
				postData.order = {
					listorder: 'desc'
				};
				var callback = function(res) {
					if (res.info.data.length > 0 && res.info.data[0]) {
						self.mainData.push.apply(self.mainData, res.info.data);
						
					};
					self.$Utils.finishFunc('getLabelData');
				};
				self.$apis.productGet(postData, callback);
			},
			
			getLabelData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					type:3,
				};
				postData.order = {
					listorder: 'desc'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.labelData.push.apply(self.labelData, res.info.data);
						self.currentId = self.labelData[0].id;
						self.getMainData(true)
					}
				};
				self.$apis.labelGet(postData, callback);
			},
			
			getSliderData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					title:"首页轮播"
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.sliderData = res.info.data[0]
					}
					self.$Utils.finishFunc('getSliderData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
		}
	};
</script>

<style>
	@import "../../assets/style/navbar.css";
	@import "../../assets/style/productList.css";
	
	page{padding-bottom: 140rpx;}	
	
	.homeHead{}
	.GpsAdrs{background-color: #222;height: 255rpx;}
	.GpsIcon{width: 30rpx;height: 36rpx;}
	
	/* .infor image{width: 100rpx;height: 100rpx;} */
	
	.swiper-box{height: 360rpx;box-shadow: 0 3px 8px rgb(222, 163, 163,0.5);}
	
	.title-xian{position: relative; z-index: 1;}
	.title-xian.on{font-size: 32rpx;font-weight: bold;}
	.title-xian.on::before{content: '';width: 0;height: 0; border-left:14rpx solid transparent ;border-right: 14rpx solid transparent ;border-bottom: 12rpx solid red;position: absolute;left:50%;bottom: 4rpx;transform: translateX(-50%); z-index: -1;}
	
	
</style>
