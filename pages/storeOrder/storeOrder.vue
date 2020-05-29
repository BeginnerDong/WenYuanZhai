<template>
	<view>
		
		<view class="topNavFix f5bj">
			<view class="orderNav bg-white d-flex j-sb a-center shadow color6">
				<view class="tt" :class="current==1?'on':''" @click="change('1')">全部</view>
				<view class="tt" :class="current==2?'on':''" @click="change('2')">待核销</view>
				<view class="tt" :class="current==3?'on':''" @click="change('3')">已核销</view>
			</view>
		</view>
		<view class="topNavH"></view>
		
		<view class="mt-3 mx-3">
			<view class="proRow">
				<view class="item mb-3" v-for="(item,index) in mainData" :key="index">
					<view class="font-24 d-flex j-sb a-center pb-2 border-bottom">
						<view class="color9">订单编号:{{item.order_no}}</view>
						<view class="red" v-if="item.transport_status==0">待核销</view>
						<view class="red" v-if="item.transport_status==2">已核销</view>
					</view>
					<view class="d-flex j-sb a-center py-2 inforLine" :data-id="item.id"
					 @click="Router.navigateTo({route:{path:'/pages/storeOrder-detail/storeOrder-detail?id='+$event.currentTarget.dataset.id}})">
						<view class="picBox d-flex a-center flex-wrap">
							<image v-for="(c_item,c_index) in item.child" :key="c_index" :src="c_item.orderItem&&c_item.orderItem[0]&&c_item.orderItem[0].snap_product&&c_item.orderItem[0].snap_product.product&&
								c_item.orderItem[0].snap_product.product.mainImg&&c_item.orderItem[0].snap_product.product.mainImg[0]?c_item.orderItem[0].snap_product.product.mainImg[0].url:''" mode=""></image>
						</view>
						<view class="rr d-flex j-end a-center">
							<image class="arrowR" src="../../static/images/about-icon4.png" mode=""></image>
						</view>
					</view>
					<view class=" d-flex j-sb a-center py-3 border-top">
						<view class="font-24 color9">{{item.create_time}}</view>
						<view>共{{item.child.length}}件商品 合计:<span class="price">{{item.price}}</span></view>
					</view>
					<view class="underBtn d-flex j-sb a-center py-3 border-top font-26">
						<view>提货单号：<span class="red">{{item.id}}</span></view>
					</view>
				</view>
			</view>
		</view>
		
		<view class="R-fixIcon"><image src="../../static/images/merchantsl-icon.png" mode="" 
		@click="scanCode"></image></view>
		
		<!-- 无数据 -->
		<view class="nodata" v-if="mainData.length==0"><image src="../../static/images/nodata.png" mode=""></image></view>
		<view class="submitbtn" style="position: fixed;bottom: 0;width: 100%;">
			<view class="btn" style="width: 100%;border-radius: 0;" @click="loginOff">退出登录</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				keywords:'',
				mainData:[],
				current:1,
				searchItem:{
					user_type:0,
					thirdapp_id:2,
					pay_status:1,
					level:1
				}
			}
		},
		
		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.searchItem.shop_no = uni.getStorageSync('merchant_info').user_no;
			//self.$Utils.loadAll(['getMainData'], self);
		},
		
		onShow() {
			const self = this;
			self.getMainData(true)
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
			
			loginOff(){
				const self = this;
				uni.removeStorageSync('merchant_info');
				uni.removeStorageSync('merchant_token');
				self.Router.redirectTo({route:{path:'/pages/user/user'}})
			},
			
			scanCode(){
				const self = this;
				uni.scanCode({
				    success: function (res) {
				        self.getOrderData(res.result)
				    }
				});
			},
			
			getOrderData(id) {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getMerchantToken';
				postData.searchItem = {
					id:id,
					user_type:0,
					shop_no:uni.getStorageSync('merchant_info').user_no
				};
				
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.Router.navigateTo({route:{path:'/pages/storeOrder-detail/storeOrder-detail?id='+res.info.data[0].id}})
					}else{
						self.$Utils.showToast('二维码无效')
					}
				};
				self.$apis.orderGet(postData, callback);
			},
			
			change(current) {
				const self = this;
				if(current!=self.current){
					self.current = current;
					if(self.current==1){
						delete self.searchItem.transport_status
					}else if(self.current==2){
						self.searchItem.transport_status = 0
					}else if(self.current==3){
						self.searchItem.transport_status = 2
					};
					self.getMainData(true)
				}
			},
			
			
			
			
			getMainData(isNew) {
				const self = this;
				console.log(2323)
				if (isNew) {
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage: 1,
						is_page: true,
						pagesize: 10
					}
				};
				const postData = {};
				postData.tokenFuncName = 'getMerchantToken';
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = self.$Utils.cloneForm(self.searchItem)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData,res.info.data)
						for (var i = 0; i < self.mainData.length; i++) {
							self.mainData[i].totalCount = 0;
							for (var j = 0; j < self.mainData[i].child.length; j++) {
								self.mainData[i].totalCount += self.mainData[i].child[j].count
							}
						}
					}
					//self.$Utils.finishFunc('getMainData');
				};
				self.$apis.orderGet(postData, callback);
			},
			
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
