<template>
	<view>
		
		<view class="userHead position-relative">
			<view class="bj"><image src="../../static/images/about-img.png" mode=""></image></view>
			<view class="infor text-white">
				<view class="text-white text-center mt-5" style="font-size: 16px;height: 40px; line-height: 40px;">我的</view>
				<view class="d-flex a-center j-sb mt-3 pt-2">
					<view class="d-flex a-center ml-3" style="width:66%;">
						<view class="photo" style="overflow: hidden;"><open-data type="userAvatarUrl"></open-data></view>
						<view style="width: 70%;">
							<view class="font-32 font-weight"><open-data type="userNickName"></open-data></view>
							<!-- <view class="font-26 mt-1">15623232323</view> -->
						</view>
					</view>
					<view class="ewmBtn d-flex j-center a-center px-1 font-24" @click="Router.navigateTo({route:{path:'/pages/userOrder/userOrder'}})"><image class="mr-1" style="width: 30rpx;height: 30rpx;" src="../../static/images/about-icon.png" mode=""></image>提货二维码</view>
				</view>
				
			</view>
		</view>
		
		<view class="myRowBetween mx-3 mt-3 bg-white rounded10 overflow-h">
			<view class="item d-flex a-center j-sb"  @click="Router.navigateTo({route:{path:'/pages/userOrder/userOrder'}})">
				<view class="ll d-flex a-center">
					<view class="icon"><image src="../../static/images/about-icon1.png" mode=""></image></view>
					<view>我的订单</view>
				</view>
				<view class="rr"><image class="arrowR" src="../../static/images/about-icon4.png" mode=""></image></view>
			</view>
			<view class="item d-flex a-center j-sb"  @click="Router.navigateTo({route:{path:'/pages/zitiAddress/zitiAddress'}})">
				<view class="ll d-flex a-center">
					<view class="icon"><image src="../../static/images/about-icon2.png" mode=""></image></view>
					<view>自提点</view>
				</view>
				<view class="rr"><image class="arrowR" src="../../static/images/about-icon4.png" mode=""></image></view>
			</view>
		</view>
		<view class="myRowBetween mx-3 mt-3 bg-white rounded10 overflow-h">
			<view class="item d-flex a-center j-sb" @click="Router.navigateTo({route:{path:'/pages/storeLogin/storeLogin'}})">
				<view class="ll d-flex a-center">
					<view class="icon"><image src="../../static/images/about-icon3.png" mode=""></image></view>
					<view>门店入口</view>
				</view>
				<view class="rr"><image class="arrowR" src="../../static/images/about-icon4.png" mode=""></image></view>
			</view>
		</view>
		<view class="submitbtn" style="margin-top: 200rpx;">
			<view class="btn" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">去购物</view>
		</view>
		
		<!--底部tab键-->
		<view class="navbar">
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<view class="nav_img">
					<image src="../../static/images/nabar1.png" />
				</view>
				<view class="text">首页</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/car/car'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar2.png" />
				</view>
				<view class="text">购物车</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar3-a.png" />
				</view>
				<view class="text this-text">我的</view>
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


		},
	};
</script>

<style>
	@import "../../assets/style/editInfor.css";
	@import "../../assets/style/navbar.css";
	page{padding-bottom: 140rpx;background: #F5F5F5;}
	
	.userHead{width: 100%;height:400rpx;background-color: #222222; z-index: 1;}
	.userHead .bj{width: 100%;height: 100%;opacity: 0.5;}
	.userHead .photo{width: 114rpx;height: 114rpx;border-radius: 50%;margin-right: 20rpx;border: 1px solid rgba(0,0,0,0.15);}
	.userHead .infor{position: absolute;top: 0; right: 0; left: 0;bottom: 0;}
	.ewmBtn{width: 200rpx;height: 60rpx;background-color: rgba(255,255,255,0.5);border-radius: 30rpx 0 0 30rpx;}
	
	.myRowBetween .item{padding: 30rpx 4%;}
	.myRowBetween .item:last-child{border-bottom: none;}
	.myRowBetween .ll .icon{width: 50rpx;height:50rpx;margin-right: 20rpx;}
	
</style>
