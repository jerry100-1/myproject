<template>
	<view class="content">
		<view v-if="salesList.length>0">
			<view class="top">
				<view class="money">销售总金额:<text class="color">￥{{money}}元</text> </view>
			</view>
			<view class="list">
				<view class="item_list" v-for="(item,index) in salesList" :key="index">
					<view>
						<text>订单完成时间:{{item.confirmTime}}</text>
						<text class="r">交易成功</text>
					</view>
					<view class="box">
						<view>
							<image :src="item.originalImg||''" v-if="item.payType==1"></image>
							<image src="../../static/pro/down.png" v-else></image>
						</view>
						<view class="left">
							<view class="title">{{item.productName||""}}</view>
							
							<view style="margin-top:-40upx;">
								<text class="price">支付方式 普通支付</text>
								<text class="r">分享雇金比例 8%</text>
							</view>
							
							
							
							<view>
								<text class="price">￥{{item.payMoney||""}}</text>
								<text class="r">x{{item.productNum||""}}</text>
							</view>
						</view>
					</view>
				</view>
				<uni-load-more :status="status"></uni-load-more>
			</view>
		</view>
		<view class="no" v-else>
			<image src="../../static/noData.png" class="noData"></image>
			<view>暂无数据</view>
		</view>
	</view>
</template>

<script>
	import uniLoadMore from "@/components/uni-load-more/uni-load-more.vue"
	export default {
		components: {uniLoadMore},
		data(){
			return{
				money:"",
				status:"loading",
				shopObj:{},
				salesList:[],
				pageNo:1,
				pageAll:2,
			}
		},
		methods:{
			search(){
				let that=this;
				if(that.pageNo<=that.pageAll){
					that.$ajax({
						url:"/fund/searchAllSalesRevenueForPage",
						data:{
							pageNo:that.pageNo,
							pageSize:20,
							searchData: {
							  marchantId: that.shopObj.merchantId
							},
						},
						success(d){
							that.pageNo=that.pageNo*1+1;
							that.pageAll=d.totalPage
							if(that.pageNo==2){
								that.salesList=d.lists
							}else{
								let arr=that.salesList;
								that.salesList=that.salesList.concat(d.lists)
							}
							if(that.pageNo>that.pageAll){
								that.status="noMore"
							}
						}
					})
				}
			}
		},
		onReachBottom(){
			this.search()
		},
		onLoad(e){
			this.money=e.money||0
		},
		onShow(){
			let that=this;
			uni.getStorage({
				key:"shopObj",
				success(res){
					that.shopObj=JSON.parse(res.data);
					that.search()
				}
			})
		},	
	}
</script>

<style scoped>
	.content{
		background: #f2f2f2;
		padding: 0;
	}
	.color{
		color:#EE3535;
	}
	.top{
		line-height: 88upx;
		padding: 0 30upx;
	}
	.item_list{
		height: 280upx;
		background: #fff;
		border-top:1px solid #eee;
	}
	.item_list>view{
		padding: 0 30upx;
		font-size: 22upx;
		margin-top: 25upx;
		
	}
	.item_list>view>.r{
		color:#EE3535;
	}
	.item_list image{
		width:164upx;
		
		height:164upx;
		margin-right: 18upx;
	}
	.box>view{
		display: inline-block;
		vertical-align: top;
	}
	.box .left{
		width:478upx
	}
	.title{
		height: 64upx;
		display: -webkit-box;
		margin: 0 auto;
		line-height: 1.4;
		-webkit-line-clamp: 2;
		-webkit-box-orient: vertical;
		overflow: hidden;
		text-overflow: ellipsis;
		margin-bottom: 70upx;
	}
	.price{
		color:#f90;
	}
</style>
