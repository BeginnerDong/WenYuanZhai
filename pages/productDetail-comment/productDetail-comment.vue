<template>
	<view>
		
		
		
		<!-- 评价 -->
		<view class="px-3">
			<view class="detail_pjLis">
				<view class="item" v-for="(item,index) in messageData" :key="index">
					<view class="d-flex j-sb a-center pb-1 font-24">
						<view class="d-flex a-center">
							<view class="photo mr-1"><image src="../../static/images/goodsl-img4.png" mode=""></image></view>
							<view class="name color6">哆啦A梦</view>		
						</view>
						<view class="time color9">2020-03-17</view>
					</view>
					<view class="text font-26 pt-1">根据瑞灵活赶紧来都搞好了电话沟通各环节的反馈给换了多个黑客帝国</view>
					<view class="picLis d-flex a-start flex-wrap">
						<view class="pic"><image src="../../static/images/goodsl-img5.png" mode=""></image></view>
						<view class="pic"><image src="../../static/images/goodsl-img5.png" mode=""></image></view>
						<view class="pic"><image src="../../static/images/goodsl-img5.png" mode=""></image></view>
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
				messageData:3
			}
		},
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
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
	@import "../../assets/style/detail.css";
	page{padding-bottom:60rpx;}
	
	
	
</style>
