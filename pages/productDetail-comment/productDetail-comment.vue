<template>
	<view>
		
		
		
		<!-- 评价 -->
		<view class="px-3">
			<view class="detail_pjLis">
				<view class="item" v-for="(item,index) in mainData" :key="index">
					<view class="d-flex j-sb a-center pb-1 font-24">
						<view class="d-flex a-center">
							<view class="photo mr-1"><image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" mode=""></image></view>
							<view class="name color6">{{item.title!=''?item.title:'用户'+item.user_no}}</view>		
						</view>
						<view class="time color9">{{item.create_time}}</view>
					</view>
					<view class="text font-26 pt-1">{{item.description}}</view>
					<view class="picLis d-flex a-start flex-wrap">
						<view class="pic" v-for="c_item in item.bannerImg">
							<image :src="c_item.url" mode=""></image>
						</view>
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
				showView: false,
				wx_info:{},
				is_show:false,
				pingjiaData:[{},{},{},{}],
				mainData:[]
			}
		},
		
		onLoad(options) {
			const self = this;
			self.product_no = options.product_no;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getMainData'], self);
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
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = {
					thirdapp_id: 2,
					product_no :self.product_no,
					type:1,
					user_type:0
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}
					console.log('23',res.info.total)
					self.totalMessage = res.info.total;
					console.log('self.mainData', self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.messageGet(postData, callback);
			},
		}
	};
</script>

<style>
	@import "../../assets/style/detail.css";
	page{padding-bottom:60rpx;}
	
	
	
</style>
