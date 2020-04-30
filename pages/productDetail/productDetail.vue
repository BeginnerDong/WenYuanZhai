<template>
	<view>
		
		<view class="detailxqBan">
			<image src="../../static/images/goodsl-img.png" />
		</view>
		
		<view class=" py-3 bg-white">
			<view class="d-flex j-sb a-center">
				<view class="price font-weight font-40 pl-3">56</view>
				<view class="shareBtn d-flex j-center a-center color9 font-24"><image style="width: 28rpx;height: 28rpx;" src="../../static/images/goodsl-icon.png" mode=""></image><view class="ml-1">分享</view></view>
			</view>
			<view class="d-flex j-sb a-center px-3 font-24 pt-2">
				<view style="color: #ff8c8c;">提货时间：次日16点-20点</view>
				<view class="color9 d-flex j-end a-center">
					<view>销量:55</view>
					<view class="ml-3">库存:55</view>
				</view>
			</view>
			<view class="mx-3 font-32 font-weight pt-3">墨西哥牛油果8枚单果200g左右</view>
		</view>
		
		<view class="px-3 bg-white rounded10 overflow-h mx-3 mt-3">
			<view class="py-3 d-flex j-sb a-center font-26 border-bottom">
				<view class="d-flex a-center">
					<view class="color6 mr-3">规格</view>
					<view>请选择商品规格</view>
				</view>
				<view class="d-flex j-end a-center" @click="spaceShow"><image class="moreIcon" src="../../static/images/goodsl-icon1.png" mode=""></image></view>
			</view>
			<view class="py-3 d-flex j-sb a-center font-26">
				<view class="d-flex a-center">
					<view class="color6 mr-3">使用方式</view>
					<view>请查看</view>
				</view>
				<view class="d-flex j-end a-center" @click="yushouTextShow"><image class="moreIcon" src="../../static/images/goodsl-icon1.png" mode=""></image></view>
			</view>
		</view>
		
		<view class=" bg-white rounded10 overflow-h mx-3 mt-3  pb-3">
			<view class=" d-flex j-sb a-center px-3 py-3">
				<view class="font-30 font-weight">商品评论</view>
				<view class="d-flex j-end a-center color9 font-24" @click="Router.navigateTo({route:{path:'/pages/productDetail-comment/productDetail-comment'}})">全部<image class="arrowR" src="../../static/images/about-icon4.png" mode=""></image></view>
			</view>
			<view class="pl-3">
				<scroll-view class="pingjia font-24 scroll-row" scroll-x>
					<view class="item mr-2 scroll-row-item" v-for="(item,index) in pingjiaData" :key="index">
						<view class="d-flex a-center">
							<view class="photo mr-2"><image src="../../static/images/goodsl-img1.png" mode=""></image></view>
							<view>龙门架</view>
						</view>
						<view class="text pt-2 avoidOverflow3">爱干净发生过热偶IG惹估计了肯定是个免费的升龙国际广发基金打卡国家饭都快过节费国际饭店科技股份可怜的感觉过分</view>
					</view>
				</scroll-view>
			</view>
		</view>
		
		<view class="R-fixIcon" @click="Router.navigateTo({route:{path:'/pages/detailShare/detailShare'}})"><image src="../../static/images/goodsl-icon4.png" mode=""></image></view>
		
		<view class="f5Bj-H20"></view>
		<view class="px-3">
			<view class="py-3 xqInfor">
				<view class="font-30 pb-3 font-weight">详情描述</view>
				<view class="cont fs14 text-center">
					<view>管理客服电话</view>
					<view>悲愤交加鹤骨鸡肤供货</view>
					<view>方点击可供货方都拉黑干活的放假</view>
					<view>价格过节费考虑到加工费</view>
					<view><image src="../../static/images/goodsl-img2.png" mode="widthFix"></image></view>
					<view>管理客服电话</view>
					<view>悲愤交加鹤骨鸡肤供货</view>
					<view>方点击可供货方都拉黑干活的放假</view>
					<view>价格过节费考虑到加工费</view>
				</view>
			</view>
		</view>
		
		<view class="xqbotomBar center pl-3">
			<view class="d-flex fs12">
				<view class="ite flexColumn" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
					<view class="icon"><image src="../../static/images/goodsl-icon2.png" mode=""></image></view>
					<view class="mt-1">首页</view>
				</view>
			</view>
			<view class="bottom-btnCont d-flex text-white font-30">
				<view class="w-50 text-center hei" @click="spaceShow">加入购物车</view>
				<view class="w-50 text-center main-bg-color" @click="spaceShow">立即购买</view>
			</view>
		</view>
		
		
		<!-- 规格选择 -->
		<view class="black-bj" v-show="is_show"></view>
		<view class="spaceShow bg-white" v-show="is_spaceShow">
			<view class="closebtn" @click="spaceShow">×</view>
			<view class="d-flex">
				<view class="pic rounded10 overflow-h mr-3"><image src="../../static/images/goodsl-img5.png" mode=""></image></view>
				<view class="infor">
					<view class="price font-weight font-36 mt-5 pt-2 mb-3">42</view>
					<view class="font-26">请选择规格</view>
				</view>
			</view>
			<view class="mt-3">
				<view class="font-26">规格</view>
				<block >
					<scroll-view scroll-y="true" >
						<view class="specsLable d-flex font-26 text-center" style="height: 320rpx; display: inline-block;">
							<view class="tt px-1" :class="specsCurr==index?'on':''" v-for="(item,index) in seltSpecsData" :key="index" @click="specsChange(index)">{{item}}</view>
						</view>
					</scroll-view>
				</block>
			</view>
			<view class="xqbotomBar px-3 mb-3" style="box-shadow:initial">
				<view class="bottom-btnCont d-flex rounded50 overflow-h text-white font-30" style="width: 100%;line-height: 80rpx;">
					<view class="w-50 text-center hei mr-1">加入购物车</view>
					<view class="w-50 text-center main-bg-color" v-show="!is_buyState" @click="Router.navigateTo({route:{path:'/pages/orderConfim/orderConfim'}})">立即购买</view>
					<!-- 不可购买弹框 -->
					<view class="w-50 text-center main-bg-color" v-show="is_buyState" @click="NoBuyShow">立即购买</view>
				</view>
			</view>
			
		</view>
		
		
		<!-- 预售说明弹框 -->
		<view class="yushouText" v-show="is_yushouTextShow">
			<view class="closebtn" @click="yushouTextShow">×</view>
			<view class="mb-3 font-30 pb-1 text-center">使用方法</view>
			<block>
				<scroll-view class="xqInfor font-26 color6 mt-3" scroll-y style="height: 80%">
					<view class="cont">
						<view>1、九是国家开发的说法是国防生的客户给发的广泛地刚刚好共同繁荣</view>
						<view>1、九是国家开发的说法是国防生的客户给发的广泛地刚刚好共同繁荣</view>
						<view>1、九是国家开发的说法是国防生的客户给发的广泛地刚刚好共同繁荣</view>
						<view>1、九是国家开发的说法是国防生的客户给发的广泛地刚刚好共同繁荣</view>
						<view>1、九是国家开发的说法是国防生的客户给发的广泛地刚刚好共同繁荣</view>
						<view>1、九是国家开发的说法是国防生的客户给发的广泛地刚刚好共同繁荣</view>
						<view>1、九是国家开发的说法是国防生的客户给发的广泛地刚刚好共同繁荣</view>
						<view>1、九是国家开发的说法是国防生的客户给发的广泛地刚刚好共同繁荣</view>
					</view>
				</scroll-view>
			</block>
		</view>
		
		<!-- 商品不可购买弹框 -->
		<view class="yushouText text-center" style="height: 780rpx;" v-show="is_NoBuyShow">
			<view class="closebtn" @click="NoBuyClose">×</view>
			<view class="pt-4">该商品不可购买，您可以购买其他的商品</view>
			<view class="j-center d-flex a-center"><image style="width: 330rpx;height: 330rpx;margin: 70rpx auto 90rpx auto;" src="../../static/images/goodsl-img3.png" mode=""></image></view>
			<view class="submitbtn">
				<view class="btn" style="border-radius: 10rpx;">去看看</view>
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
				wx_info:{},
				is_show:false,
				specsCurr:0,
				pingjiaData:3,
				is_spaceShow:false,
				seltSpecsData:['大份','中份','小芬','大份','中份','小芬'],
				is_yushouTextShow:false,
				is_NoBuyShow:false,
				is_buyState:false
			}
		},
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			specsChange(index){
				const self = this;
				self.specsCurr = index
			},
			spaceShow(){
				const self = this;
				self.is_show = !self.is_show;
				self.is_spaceShow = !self.is_spaceShow 
			},
			yushouTextShow(){
				const self = this;
				self.is_show = !self.is_show;
				self.is_yushouTextShow = !self.is_yushouTextShow 
			},
			
			// 不可购买弹框
			NoBuyShow(){
				const self = this;
				self.is_show = true;
				self.is_NoBuyShow = true
				self.is_spaceShow = !self.is_spaceShow 
			},
			NoBuyClose(){
				const self = this;
				self.is_show = false;
				self.is_NoBuyShow = false
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
	@import "../../assets/style/orderNav.css";
	@import "../../assets/style/detail.css";
	@import "../../assets/style/productList.css";
	page{padding-bottom:140rpx;background-color: #F5F5F5;}
	
	.shareBtn{background: #F5F5F5;width: 120rpx;height: 44rpx;border-radius: 25rpx 0 0 25rpx;}
	
	.bottom-btnCont{width: 560rpx;line-height: 100rpx;}
	.bottom-btnCont .hei{background-color: #3c3c3c;}
	
	.specsLable{flex-wrap: wrap;}
	.specsLable .tt{float: left;margin: 30rpx 50rpx 0 0;border: 1px solid #F5F5F5;line-height: 60rpx;border-radius:10rpx;min-width: 170rpx;background-color: #F5F5F5;}
	
	.specsLable .tt.on{background-color: #ffe3e3;color: #db1b1b;border: 1px solid #db1b1b;}
	
	.spaceShow{width: 100%;border-radius: 20rpx 20rpx 0 0;position: fixed;left: 0;right: 0;bottom: 0;height: 800rpx;z-index: 50;padding: 30rpx;padding-bottom: 140rpx;}
	.spaceShow .pic{width: 210rpx;height: 210rpx;}
	
	.yushouText{height:75%;width: 90%;background-color: #fff;border-radius: 10rpx;position: fixed;top: 50%;left: 50%;transform: translate(-50%,-50%);box-sizing: border-box;padding: 30rpx;z-index: 50;}
	
	.moreIcon{width: 44rpx;height: 8rpx;}
	
	/* 评价 */
	.pingjia .item{width: 500rpx;height: 255rpx;border-radius: 10rpx;background-color: #F5F5F5;padding: 20rpx;}
	.pingjia .item .photo{width: 60rpx;height: 60rpx;border-radius: 50%;}
	.pingjia .item .text{white-space: initial;}
	
</style>
