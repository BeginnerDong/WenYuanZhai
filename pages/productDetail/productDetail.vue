<template>
	<view>

		<view class="detailxqBan">
			<image :src="mainData.bannerImg&&mainData.bannerImg[0]?mainData.bannerImg[0].url:''" />
		</view>

		<view class=" py-3 bg-white">
			<view class="d-flex j-sb a-center">
				<view class="price font-weight font-40 pl-3">{{mainData.price}}</view>
				<button style="margin: 0;padding: 0;" open-type="share" class="shareBtn d-flex j-center a-center color9 font-24">
					<image style="width: 28rpx;height: 28rpx;" src="../../static/images/goodsl-icon.png" mode="">

					</image>
					<view class="ml-1">分享</view>
				</button>
			</view>
			<view class="d-flex j-sb a-center px-3 font-24 pt-2">
				<view style="color: #ff8c8c;">提货时间：{{pickTime}}</view>
				<view class="color9 d-flex j-end a-center">
					<view>销量:{{mainData.sale_count?mainData.sale_count:'0'}}</view>
					<!-- <view class="ml-3">库存:{{mainData.stock?mainData.stock:'0'}}</view> -->
				</view>
			</view>
			<view class="mx-3 font-32 font-weight pt-3">{{mainData.title}}</view>
		</view>

		<view class="px-3 bg-white rounded10 overflow-h mx-3 mt-3">
			<view class="py-3 d-flex j-sb a-center font-26" @click="spaceShow">
				<view class="d-flex a-center">
					<view class="color6 mr-3">规格</view>
					<view>{{mainData.sku[specsCurr]?'已选'+mainData.sku[specsCurr].title:'选择商品规格'}}</view>
				</view>
				<view class="d-flex j-end a-center">
					<image class="moreIcon" src="../../static/images/goodsl-icon1.png" mode=""></image>
				</view>
			</view>
			<!-- <view class="py-3 d-flex j-sb a-center font-26">
				<view class="d-flex a-center">
					<view class="color6 mr-3">使用方式</view>
					<view>请查看</view>
				</view>
				<view class="d-flex j-end a-center" @click="yushouTextShow">
					<image class="moreIcon" src="../../static/images/goodsl-icon1.png" mode=""></image>
				</view>
			</view> -->
		</view>

		<view class=" bg-white rounded10 overflow-h mx-3 mt-3  pb-3">
			<view class=" d-flex j-sb a-center px-3 py-3">
				<view class="font-30 font-weight">商品评论</view>
				<view class="d-flex j-end a-center color9 font-24" @click="Router.navigateTo({route:{path:'/pages/productDetail-comment/productDetail-comment?product='+mainData.product_no}})">全部<image
					 class="arrowR" src="../../static/images/about-icon4.png" mode=""></image>
				</view>
			</view>
			<view class="pl-3">
				<scroll-view class="pingjia font-24 scroll-row" scroll-x v-if="messageData.length>0">
					<view class="item mr-2 scroll-row-item" v-for="(item,index) in messageData" :key="index">
						<view class="d-flex a-center">
							<view class="photo mr-2">
								<image :src="item.mainImg&&item.mainImg[0]&&item.mainImg[0].url!=''?item.mainImg[0].url:''" mode=""></image>
							</view>
							<view>{{item.title!=''?item.title:'用户'}}</view>
						</view>
						<view class="text pt-2 avoidOverflow3">{{item.description}}</view>
					</view>

				</scroll-view>
				<view class="text-center" v-else>暂无评论</view>
			</view>
		</view>

		<view class="R-fixIcon" @tap="shareEvn">
			<image src="../../static/images/goodsl-icon4.png" mode=""></image>
		</view>

		<view class="f5Bj-H20"></view>
		<view class="px-3">
			<view class="py-3 xqInfor">
				<view class="font-30 pb-3 font-weight">详情描述</view>
				<view class="cont fs14 text-center">
					<view class="content ql-editor" style="padding:0;" v-html="mainData.content">
					</view>
				</view>
			</view>
		</view>

		<view class="xqbotomBar center pl-3">
			<view class="d-flex fs12">
				<view class="ite flexColumn" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
					<view class="icon">
						<image src="../../static/images/goodsl-icon2.png" mode=""></image>
					</view>
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
				<view class="pic rounded10 overflow-h mr-3">
					<image :src="mainData.sku[specsCurr]&&mainData.sku[specsCurr].mainImg&&mainData.sku[specsCurr].mainImg[0]
					?mainData.sku[specsCurr].mainImg[0].url:''"
					 mode=""></image>
				</view>
				<view class="infor">
					<view class="price font-weight font-36 mt-5 pt-2 mb-3">{{mainData.sku[specsCurr]?mainData.sku[specsCurr].price:''}}</view>
					<view class="font-26">库存：{{mainData.sku[specsCurr]?mainData.sku[specsCurr].stock:'0'}}</view>
				</view>
			</view>
			<view class="mt-3">
				<view class="font-26">规格</view>
				<block>
					<scroll-view scroll-y="true">
						<view class="specsLable d-flex font-26 text-center" style="height: 320rpx; display: inline-block;">
							<view class="tt px-1" :class="specsCurr==index?'on':''" v-for="(item,index) in mainData.sku" :key="index" @click="specsChange(index)">{{item.title}}</view>
						</view>
					</scroll-view>
				</block>
			</view>
			<view class="xqbotomBar px-3 mb-3" style="box-shadow:initial">
				<view class="bottom-btnCont d-flex rounded50 overflow-h text-white font-30" style="width: 100%;line-height: 80rpx;">
					<view class="w-50 text-center hei mr-1" @click="addCar">加入购物车</view>

					<!-- 不可购买弹框 -->
					<view class="w-50 text-center main-bg-color" @click="goBuy">立即购买</view>
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
						<view class="content ql-editor" style="padding:0;" v-html="mainData.instructions">
						</view>
					</view>
				</scroll-view>
			</block>
		</view>

		<!-- 商品不可购买弹框 -->
		<view class="yushouText text-center" style="height: 780rpx;" v-show="is_NoBuyShow">
			<view class="closebtn" @click="NoBuyClose">×</view>
			<view class="pt-4">店家已休息，明天再来购买吧</view>
			<view class="j-center d-flex a-center">
				<image style="width: 330rpx;height: 330rpx;margin: 70rpx auto 90rpx auto;" src="../../static/images/goodsl-img3.png"
				 mode=""></image>
			</view>
			<!-- <view class="submitbtn">
				<view class="btn" style="border-radius: 10rpx;">去看看</view>
			</view> -->
		</view>
		<hchPoster ref="hchPoster" :canvasFlag.sync="canvasFlag" @cancel="canvasCancel" :posterObj.sync="posterData" />
		<view :hidden="canvasFlag">
			<!-- 海报 要放外面放组件里面 会找不到 canvas-->
			<canvas class="canvas" canvas-id="myCanvas"></canvas><!-- 海报 -->
		</view>

		<view class="share-pro" v-if="deliveryFlag">
			<view class="share-pro-mask"></view>
			<view class="share-pro-dialog" :class="deliveryFlag?'open':'close'">
				<view class="close-btn" @tap="closeShareEvn">
					<span class="font_family">&#xe6e6;</span>
				</view>
				<view class="share-pro-title">分享</view>
				<view class="share-pro-body">
					<view class="share-item">
						<button open-type="share">
							<view class="font_family share-icon">&#xe6fa;</view>
							<view>分享给好友</view>
						</button>
					</view>
					<view class="share-item" @tap="createCanvasImageEvn">
						<view class="font_family share-icon">&#xe6f9;</view>
						<view>生成分享图片</view>
					</view>
				</view>

			</view>
		</view>
	</view>
</template>

<script>
	import hchPoster from '../../wxcomponents/hch-poster/hch-poster.vue'
	export default {
		components: {
			hchPoster,
		},
		data() {
			return {
				Router: this.$Router,
				showView: false,
				wx_info: {},
				is_show: false,
				specsCurr: 0,
				pingjiaData: 3,
				is_spaceShow: false,
				seltSpecsData: ['大份', '中份', '小芬', '大份', '中份', '小芬'],
				is_yushouTextShow: false,
				is_NoBuyShow: false,
				is_buyState: false,
				canBuy: false,
				mainData: {},
				orderList: [],
				pickTime: '',
				messageData: [],
				canvasFlag: true,
				deliveryFlag: false,
				posterData: {}
			}
		},

		onLoad(options) {
			const self = this;
			if(options.id){
				self.id = options.id;
			}else if(options.scene){
				self.id = decodeURIComponent(options.scene)
			};
			
			self.$Utils.loadAll(['getMainData', 'getQrData'], self);
		},

		onShow() {
			const self = this;
			self.orderList = [];
			uni.removeStorageSync('payPro');
		},

		onShareAppMessage(ops) {
			console.log(ops)
			const self = this;
			if (ops.from === 'button') {
				return {
					title: self.mainData.title,
					path: '/pages/productDetail/productDetail?id=' + self.mainData.id, //点击分享的图片进到哪一个页面
					imageUrl: self.mainData.mainImg[0].url ? self.mainData.mainImg[0].url : '',
					success: function(res) {
						// 转发成功
						console.log("转发成功:" + JSON.stringify(res));
					},
					fail: function(res) {
						// 转发失败
						console.log("转发失败:" + JSON.stringify(res));
					}
				}
			} else {
				return {
					title: self.mainData.title,
					path: '/pages/productDetail/productDetail?id=' + self.mainData.id, //点击分享的图片进到哪一个页面
					imageUrl: self.mainData.mainImg[0].url ? self.mainData.mainImg[0].url : '',
					success: function(res) {
						// 转发成功
						console.log("转发成功:" + JSON.stringify(res));
					},
					fail: function(res) {
						// 转发失败
						console.log("转发失败:" + JSON.stringify(res));
					}
				}
				console.log(ops.target)
			}
		},

		methods: {

			getQrData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken'
				postData.qrInfo = {
					scene: self.id,
					page: 'pages/productDetail/productDetail',
				};
				postData.output = 'url';
				postData.ext = 'png';
				const callback = (res) => {
					if (res.solely_code == 100000) {
						self.QrData = res;
					} else {
						self.$Utils.showToast(res.msg, 'none')
					}
					self.$Utils.finishFunc('getQrData');
				};
				self.$apis.getQrCode(postData, callback);
			},

			createCanvasImageEvn() {
				const self = this;
				
				Object.assign(this.posterData, {
					url: self.mainData.mainImg[0]?self.mainData.mainImg[0].url:'', //商品主图
					icon: 'https://img0.zuipin.cn/mp_zuipin/poster/hch-hyj.png', //醉品价图标
					title: self.mainData.title, //标题
					discountPrice: self.mainData.price, //折后价格
					//orignPrice: "300.00", //原价
					code: self.QrData.info.url, //小程序码
				})
				this.$forceUpdate(); //强制渲染数据
				setTimeout(() => {
					this.canvasFlag = false; //显示canvas海报
					this.deliveryFlag = false; //关闭分享弹窗
					this.$refs.hchPoster.createCanvasImage(); //调用子组件的方法
				}, 1000)
			},

			// 分享弹窗
			shareEvn() {
				this.deliveryFlag = true;
				console.log(this.deliveryFlag)
			},
			// 关闭分享弹窗
			closeShareEvn() {
				this.deliveryFlag = false;
			},
			// 取消海报
			canvasCancel(val) {
				this.canvasFlag = val;
			},

			getMainData() {
				const self = this;
				var now = new Date().getTime();
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					id: self.id
				};
				postData.getAfter = {
					sku: {
						tableName: 'Sku',
						middleKey: 'product_no',
						key: 'product_no',
						condition: '=',
						searchItem: {
							status: 1
						}
					},
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						var d = new Date();
						var h = d.getHours();
						console.log('h',h)
						if (h >= uni.getStorageSync('user_info').thirdApp.start_time && h < uni.getStorageSync('user_info').thirdApp.end_time) {
							self.canBuy = true
						};
						const regex = new RegExp('<img', 'gi');
						self.mainData.content = self.mainData.content.replace(regex, `<img style="max-width: 100%;"`);
						self.mainData.instructions = self.mainData.instructions.replace(regex, `<img style="max-width: 100%;"`);
						self.pickTime = '次日' + uni.getStorageSync('user_info').thirdApp.pickup_start + '点-' + uni.getStorageSync(
							'user_info').thirdApp.pickup_end + '点'
					};
					self.getMessageData();
					self.$Utils.finishFunc('getMainData');

				};
				self.$apis.productGet(postData, callback);
			},

			goBuy() {
				const self = this;
				uni.setStorageSync('canClick', false);
				if (!self.canBuy) {
					uni.setStorageSync('canClick', true);
					self.NoBuyShow();
					return
				};
				if (self.mainData.sku.length==0) {
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('该商品暂无可选规格', 'none');
					return
				};
				self.orderList.push({
					sku_id: self.mainData.sku[self.specsCurr].id,
					count: 1,
					type: self.mainData.type,
					product: self.mainData,
					skuIndex: self.specsCurr
				}, );
				uni.setStorageSync('payPro', self.orderList);
				self.Router.navigateTo({
					route: {
						path: '/pages/orderConfim/orderConfim'
					}
				})
				uni.setStorageSync('canClick', true);
			},

			addCar() {
				const self = this;
				if (!self.canBuy) {
					uni.setStorageSync('canClick', true);
					self.NoBuyShow();
					return
				};
				if (self.mainData.sku.length==0) {
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('该商品暂无可选规格', 'none');
					return
				};
				var obj = self.mainData;
				self.mainData.skuIndex = self.specsCurr;
				var array = self.$Utils.getStorageArray('cartData');
				for (var i = 0; i < array.length; i++) {
					if (array[i].sku[array[i].skuIndex].id == self.mainData.sku[self.specsCurr].id) {
						var target = array[i]
					}
				}
				if (target) {
					target.count = target.count + 1
				} else {
					var target = self.mainData;
					target.count = 1;
					target.isSelect = true;
				}
				self.$Utils.showToast('加入成功', 'none');
				self.$Utils.setStorageArray('cartData', target, 'id', 999);
			},

			getMessageData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.paginate = {
					count: 0,
					currentPage: 1,
					is_page: true,
					pagesize: 3
				};
				postData.searchItem = {
					thirdapp_id: 2,
					product_no: self.mainData.product_no,
					type: 1,
					user_type: 0
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.messageData.push.apply(self.messageData, res.info.data);
					}
					console.log('self.messageData', self.messageData)
					self.$Utils.finishFunc('getMessageData');
				};
				self.$apis.messageGet(postData, callback);
			},

			specsChange(index) {
				const self = this;
				self.specsCurr = index
			},
			spaceShow() {
				const self = this;
				self.is_show = !self.is_show;
				self.is_spaceShow = !self.is_spaceShow
			},
			yushouTextShow() {
				const self = this;
				self.is_show = !self.is_show;
				self.is_yushouTextShow = !self.is_yushouTextShow
			},

			// 不可购买弹框
			NoBuyShow() {
				const self = this;
				self.is_show = true;
				self.is_NoBuyShow = true
				self.is_spaceShow = !self.is_spaceShow
			},
			NoBuyClose() {
				const self = this;
				self.is_show = false;
				self.is_NoBuyShow = false
			},

		}
	};
</script>

<style lang="scss">
	@import "../../assets/style/orderNav.css";
	@import "../../assets/style/detail.css";
	@import "../../assets/style/productList.css";

	page {
		padding-bottom: 140rpx;
		background-color: #F5F5F5;
	}

	.shareBtn {
		background: #F5F5F5;
		width: 120rpx;
		height: 44rpx;
		border-radius: 25rpx 0 0 25rpx;
	}

	.bottom-btnCont {
		width: 560rpx;
		line-height: 100rpx;
	}

	.bottom-btnCont .hei {
		background-color: #3c3c3c;
	}

	.specsLable {
		flex-wrap: wrap;
	}

	.specsLable .tt {
		float: left;
		margin: 30rpx 50rpx 0 0;
		border: 1px solid #F5F5F5;
		line-height: 60rpx;
		border-radius: 10rpx;
		min-width: 170rpx;
		background-color: #F5F5F5;
	}

	.specsLable .tt.on {
		background-color: #ffe3e3;
		color: #db1b1b;
		border: 1px solid #db1b1b;
	}

	.spaceShow {
		width: 100%;
		border-radius: 20rpx 20rpx 0 0;
		position: fixed;
		left: 0;
		right: 0;
		bottom: 0;
		height: 800rpx;
		z-index: 50;
		padding: 30rpx;
		padding-bottom: 140rpx;
	}

	.spaceShow .pic {
		width: 210rpx;
		height: 210rpx;
	}

	.yushouText {
		height: 75%;
		width: 90%;
		background-color: #fff;
		border-radius: 10rpx;
		position: fixed;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		box-sizing: border-box;
		padding: 30rpx;
		z-index: 50;
	}

	.moreIcon {
		width: 44rpx;
		height: 8rpx;
	}

	/* 评价 */
	.pingjia .item {
		width: 500rpx;
		height: 255rpx;
		border-radius: 10rpx;
		background-color: #F5F5F5;
		padding: 20rpx;
	}

	.pingjia .item .photo {
		width: 60rpx;
		height: 60rpx;
		border-radius: 50%;
	}

	.pingjia .item .text {
		white-space: initial;
	}

	@font-face {
		font-family: 'font_family';
		/* project id 1065286 */
		src: url('//at.alicdn.com/t/font_1065286_3bsye5aijur.eot');
		src: url('//at.alicdn.com/t/font_1065286_3bsye5aijur.eot?#iefix') format('embedded-opentype'),
			url('//at.alicdn.com/t/font_1065286_3bsye5aijur.woff2') format('woff2'),
			url('//at.alicdn.com/t/font_1065286_3bsye5aijur.woff') format('woff'),
			url('//at.alicdn.com/t/font_1065286_3bsye5aijur.ttf') format('truetype'),
			url('//at.alicdn.com/t/font_1065286_3bsye5aijur.svg#font_family') format('svg');
	}

	.font_family {
		font-family: "font_family" !important;
		font-size: 16px;
		font-style: normal;
		-webkit-font-smoothing: antialiased;
		-webkit-text-stroke-width: 0.2px;
		-moz-osx-font-smoothing: grayscale;
	}

	/* 按钮去掉边框 */
	button::after {
		border: none;
	}

	button {
		margin-left: 0;
		margin-right: 0;
		padding-left: 0;
		padding-right: 0;
		line-height: 1;
		color: #1c1c1c;
		font-size: 28rpx;
		background: none;
	}

	.button-hover {
		color: #1c1c1c;
		background: none;
	}

	/*每个页面公共css */
	.content {
		text-align: center;
		height: 100%;
	}

	/* .share-btn {
		padding: 30upx 60upx;background-color: $uni-btn-color;color: $uni-text-color-inverse;
	} */

	.share-pro {
		display: flex;
		align-items: center;
		justify-content: flex-end;
		flex-direction: column;
		z-index: 5;
		line-height: 1;
		box-sizing: border-box;

		.share-pro-mask {
			width: 100%;
			height: 100%;
			position: fixed;
			top: 0;
			right: 0;
			bottom: 0;
			left: 0;
			background: rgba(0, 0, 0, 0.5);
		}

		.share-pro-dialog {
			width: 750rpx;
			height: 310rpx;
			overflow: hidden;
			background-color: #fff;
			border-radius: 24rpx 24rpx 0px 0px;
			position: relative;
			box-sizing: border-box;
			position: fixed;
			bottom: 100rpx;

			.close-btn {
				padding: 20rpx 15rpx;
				position: absolute;
				top: 0rpx;
				right: 29rpx;
			}

			.share-pro-title {
				font-size: 28rpx;
				color: #1c1c1c;
				padding: 28rpx 41rpx;
				background-color: #f7f7f7;
			}

			.share-pro-body {
				display: flex;
				flex-direction: row;
				justify-content: space-around;
				font-size: 28rpx;
				color: #1c1c1c;

				.share-item {
					display: flex;
					flex-direction: column;
					justify-content: center;
					justify-content: space-around;

					.share-icon {
						text-align: center;
						font-size: 70rpx;
						margin-top: 39rpx;
						margin-bottom: 16rpx;
						color: #42ae3c;
					}

					&:nth-child(2) {
						.share-icon {
							color: #ff5f33;
						}
					}
				}
			}
		}

		/* 显示或关闭内容时动画 */

		.open {
			transition: all 0.3s ease-out;
			transform: translateY(0);
		}

		.close {
			transition: all 0.3s ease-out;
			transform: translateY(310rpx);
		}

	}

	.canvas {
		position: fixed !important;
		top: 0 !important;
		left: 0 !important;
		display: block !important;
		width: 100% !important;
		height: 100% !important;
		z-index: 10;
	}
</style>
