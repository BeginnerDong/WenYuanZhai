<template>
	<view>
		
		<view class="homeHead position-relative">
			<view class="px-3 py-3 d-flex text-white GpsAdrs a-start">
				<view class="GpsIcon mr-1"><image src="../../static/images/home-icon.png" mode=""></image></view>
				<view>高新大都会</view>
			</view>
			<view class="banner-box px-3" style="margin-top: -160rpx;" >
				<swiper class="swiper-box rounded10 overflow-h" indicator-dots="true" autoplay="true" interval="3000" duration="1000" indicator-color="#d89c9c" indicator-active-color="#db1b1b">
					<block v-for="(item,index) in labelData" :key="index">
						<swiper-item class="swiper-item">
							<image :src="item" class="slide-image" />
						</swiper-item>
					</block>
				</swiper>
			</view>
		</view>
		
		<view class="px-3 mt-4">
			<view class="d-flex  a-center">
				<view class="title-xian mr-4 pb-2" :class="curr==1?'on':''" @click="currChange(1)">热菜</view>
				<view class="title-xian mr-4 pb-2" :class="curr==2?'on':''" @click="currChange(2)">凉菜</view>
				<view class="title-xian mr-4 pb-2" :class="curr==3?'on':''" @click="currChange(3)">主食</view>
			</view>
			
			<view class="productList">
				<view class="item py-3 border-bottom" v-for="(item,index) in productData" :key="index" @click="Router.navigateTo({route:{path:'/pages/productDetail/productDetail'}})">
					<view class="pic rounded10 overflow-h position-relative">
						<view class="fixState no" style="background-color: #7d7d7d;">不可买</view>
						<view class="fixState"  style="background-color: #37c25b;">可买</view>
						<image class="img" src="../../static/images/home-img.png" mode=""></image>
						<view class="imgTit text-white font-23 text-center avoidOverflow px-3">本商品由生灵商行专供</view>
					</view>
					<view class="infor mt-3">
						<view class="tit avoidOverflow2 font-30 font-weight">墨西哥牛油果8枚单果200g左右</view>
						<view class="price font-32 font-weight mt-1">56</view>
					</view>
				</view>
			</view>
			
			<!-- 无数据 -->
			<view class="nodata"><image src="../../static/images/nodata.png" mode=""></image></view>
			
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
				is_show: false,
				wx_info:{},
				is_show:false,
				labelData: [
					"../../static/images/home-banner.png",
					"../../static/images/home-banner.png",
					"../../static/images/home-banner.png"
				],
				curr:1,
				productData:4
			}
		},
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			currChange(curr){
				const self = this;
				if(curr!=self.curr){
					self.curr = curr
				}
			},
			
			getMainData() {
				const self = this;
				console.log('852369')
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				self.$apis.orderGet(postData, callback);
			}
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
	
	.swiper-box{height: 360rpx;box-shadow: 0 3px 8px rgb(222, 163, 163,0.5);}
	
	.title-xian{position: relative; z-index: 1;}
	.title-xian.on{font-size: 32rpx;font-weight: bold;}
	.title-xian.on::before{content: '';width: 0;height: 0; border-left:14rpx solid transparent ;border-right: 14rpx solid transparent ;border-bottom: 12rpx solid red;position: absolute;left:50%;bottom: 4rpx;transform: translateX(-50%); z-index: -1;}
	
	
</style>
