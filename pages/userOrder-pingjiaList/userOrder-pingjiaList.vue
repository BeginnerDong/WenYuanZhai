<template>
	<view>
		<view class="proRow mt-3">
			<view class="item mb-2 rounded10" >
				<view class="" v-for="(item,index) in mainData.child" :key="index">
					<view class="d-flex j-sb a-center mb-3">
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
					<view class="underBtn d-flex j-end a-center pt-3 border-top" v-if="item.isremark==0">
						<view class="Bbtn"  :data-id="item.id" @click="Router.navigateTo({route:{path:'/pages/userOrder-pingjia/userOrder-pingjia?id='+$event.currentTarget.dataset.id}})">去评价</view>
					</view>
					<view class="underBtn d-flex j-end a-center pt-3 border-top" v-if="item.isremark==1">
						<view class="Bbtn">已评价</view>
					</view>
				</view>
			</view>
		</view>	
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				mainData:{}
			}
		},
		
		onLoad(options) {
			const self = this;
			self.id = options.id;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					id: self.id,
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
	page{background: #F5F5F5;padding-bottom: 60rpx;}
</style>
