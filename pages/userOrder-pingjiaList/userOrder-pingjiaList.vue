<template>
	<view>
		<view class="mx-3 mt-3">
			<view class="proRow">
				<view class="item mb-3" v-for="(item,index) in mainData" :key="index">
					<view class="font-24 d-flex j-sb a-center pb-2 border-bottom">
						<view class="color9">订单编号:152565622323</view>
						<view class="red">已提货</view>
					</view>
					<view class="d-flex j-sb a-center py-2 inforLine">
						<view class="picBox d-flex a-center flex-wrap">
							<image src="../../static/images/shopping-img.png" mode=""></image>
						</view>
						<view class="rr d-flex j-end a-center">
							<image class="arrowR" src="../../static/images/about-icon4.png" mode=""></image>
						</view>
					</view>
					<view class=" d-flex j-sb a-center py-3 border-top">
						<view class="font-24 color9">2020.04.30 10:02</view>
						<view>共3件商品 合计:<span class="price">56</span></view>
					</view>
					<view class="underBtn d-flex j-end a-center pt-3 border-top">
						<view class="Bbtn"  @click="Router.navigateTo({route:{path:'/pages/userOrder-pingjia/userOrder-pingjia'}})">去评价</view>
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
				mainData:3
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
	page{background: #F5F5F5;padding-bottom: 60rpx;}
</style>
