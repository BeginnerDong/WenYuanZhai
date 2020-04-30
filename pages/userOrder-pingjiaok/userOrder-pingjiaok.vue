<template>
	<view>
		
		<view class="mx-3">
			<view class="proRow">
				<view class="item mt-3" v-for="(item,index) in mainData" :key="index">
					<view class="font-24 d-flex j-sb a-center pb-2 border-bottom">
						<view class="color9">订单编号:152565622323</view>
						<view class="red">已评价</view>
					</view>
					<view class="d-flex j-sb a-center py-2 inforLine border-bottom">
						<view class="picBox d-flex a-center flex-wrap">
							<image src="../../static/images/shopping-img.png" mode=""></image>
						</view>
					</view>
					<view class="f5bj rounded10 p-2 font-24 mt-2">
						<view>很反感娄山关路是个凡人的洛杉矶经历过购房即可看到据国家风口浪尖加工费考虑到国家反馈的结果了</view>
						<view class="picBox d-flex a-center flex-wrap mt-1">
							<image src="../../static/images/shopping-img.png" mode=""></image>
							<image src="../../static/images/shopping-img.png" mode=""></image>
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
				score:'',
				wx_info:{},
				mainData:2
			}
		},
		onLoad() {
			const self = this;
			//self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
		}
	};
</script>

<style>
	@import "../../assets/style/proRow.css";
	page{background: #F5F5F5;padding-bottom:30rpx;}
	
	.proRow .item .picBox{width: 100%;}
	
</style>
