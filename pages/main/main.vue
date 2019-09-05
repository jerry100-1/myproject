<template>
	<view class="content">
		<!-- <view class="top"></view> -->
		<view class="uni-page-head">
			<view class="l" style="visibility:hidden;">
				<image src="../../static/logo@2x.png" alt="" class="logo"></image>
			</view>
			<view class="center">
				我的店
			</view>
			<view class="r">
				  <view @tap="url" data-url="/pages/enter/briefIntroduction" style="width:140upx;" class="rightTextMsg">商户简介</view>
				
			<!-- 	<view @tap="changeDown">
					<image src="../../static/home/addpng.png" class="add" mode="widthFix" ></image>
				</view>
				<view @tap="url" data-url="/pages/system/system">
					<image src="../../static/home/system.png" class="system" mode="widthFix"  ></image>
				</view>
				<view class="down" v-if="isDown">
					<view class="up"></view>
					<view class="border" @tap="url" data-url="/pages/wx/wxReceipt" v-if="isPayQR">
						微信收款
					</view>
					<view class="border" @tap="urlCode" data-url="/pages/wx/channel" v-if="shopObj.level*1<3">
						渠道邀请
					</view>
					<view class="border" @tap="urlCode" data-url="/pages/wx/userInvitation">
						用户邀请
					</view>
				</view> -->
				
			</view>
		</view>
		
		<view class="shopInfo">
			<view class="img">
				<image :src="shopObj.disPlayImg" @tap="changeImg"></image>
			</view>
			<view>
				<view>{{shopObj.shopName}}</view>
				<view>上次登录:{{shopObj.loginTime}}</view>
			</view>
			<view class="r">
				<view>
					{{shopObj.levelName}} （{{shopObj.levelName=="C"?'事业部':shopObj.levelName=="B"?'互信版':shopObj.levelName=="A2"?'互爱版':'愉悦版'}}）
				</view>
			</view>
		</view>
		<view class="proList">
			<view v-for="(item,index) in textInfo.imgs" :key="index">
				<image :src="item"></image>
			</view>
		</view>
		<view class="textInfo">
			<view>
				<view>
					<text>{{textInfo.memberCount}}</text>
					<view class="text">用户总数</view>
				</view>
				<view>
					<text>{{textInfo.orderCount}}</text>
					<view class="text">订单总数</view>
				</view>
				<view>
					<text>{{textInfo.sellAmount}}</text>
					<view class="text">销售金额</view>
				</view>
				<view>
					<text>{{textInfo.collectCount}}</text>
					<view class="text">收藏总数</view>
				</view>
			</view>
			<view>
				<view v-if="shopObj.level*1<3">
					<text>{{textInfo.aChannelCount}}</text>
					<view class="text">渠道A数</view>
				</view>
			<!-- 	<view  v-if="shopObj.level*1<3">
					<text>{{textInfo.a2ChannelCount}}</text>
					<view class="text">渠道A2数</view>
				</view> -->
				<view  v-if="shopObj.level*1<2">
					<text>{{textInfo.bChannelCount}}</text>
					<view class="text">渠道B数</view>
				</view>
				<!-- <view>
					<text>{{textInfo.browseCount}}</text>
					<view class="text">浏览总数</view>
				</view> -->
			</view>
		</view>
		<view class="banner">
			<image src="/static/home/banner.png" alt="" mode="widthFix"></image>
		</view>
		<view class="enter">
			<view>
				
				<view @tap="url" data-url="/pages/user/userAdmin">
					<view class="enter_item bg1">
						<image class="image1" src="/static/home/user.png" style="margin-top:-1upx;" alt="" mode="widthFix"></image>
						<text class="newTextDesc" style="padding-top:20upx;">用户</text>
						<image   @click.stop="clickTap" data-index="1" src="/static/addImg/icon_tips@2x.png" style="width:15px;height:15px;z-index:0;"     class="rightImgAb" mode="widthFix"></image>
					
					    <view  v-if="this.index==1" class="addNewView">
							 商家直属用户,下级关联用户,交易用户的管理专区,还可对订单评论进行查看,回复等；
						</view>
					
					
					
					</view>
				</view>
				
				<view>
					<view class="enter_item bg2" @tap="url" data-url="/pages/pro/index">
						<image class="image1" style="margin-top:-1upx;" src="/static/home/shop.png" alt="" mode="widthFix"></image>
						<text class="newTextDesc" style="padding-top:20upx;">商品</text>
						<image   @click.stop="clickTap" data-index="2" src="/static/addImg/icon_tips@2x.png" style="width:15px;height:15px;z-index:0;"     class="rightImgAb" mode="widthFix"></image>
											
						<view  v-if="this.index==2" class="addNewView">
							发布商品至商家在乐驿享的专属店铺进行线上销售;对出售中,待审核,审核失败的商品进行管理；
						</view>	
					</view>
				</view>
				<view>
					<view class="enter_item bg3" @tap="url" data-url="/pages/order/orderList">
						<image class="image1" style="margin-top:-1upx;" src="/static/home/order.png" alt="" mode="widthFix"></image>
						<text class="newTextDesc" style="padding-top:20upx;">订单</text>
						<image   @click.stop="clickTap" data-index="3" src="/static/addImg/icon_tips@2x.png" style="width:15px;height:15px;z-index:0;"     class="rightImgAb" mode="widthFix"></image>
											
						<view  v-if="this.index==3" class="addNewView">
							对线上订单和线下订单进行查询,管理,发货,跟踪,对退款订单进行及时处理等;
						</view>	
					</view>
				</view>
				 
				 <view>
				 	<view class="enter_item bg4" @tap="url" data-url="/pages/capital/index">
				 		<image class="image1" style="margin-top:-1upx;" src="/static/home/capt.png" alt="" mode="widthFix"></image>
				 		<text class="newTextDesc" style="padding-top:20upx;">资金</text>
						<image   @click.stop="clickTap" data-index="4" src="/static/addImg/icon_tips@2x.png" style="width:15px;height:15px;z-index:0;"     class="rightImgAb" mode="widthFix"></image>
											
						<view  v-if="this.index==4" class="addNewView">
							销售收入,用户返佣,注册奖励,交易补贴的提现;收入金额,发放金额,提现金额的明细报表
						</view>	
				 	</view>
				 </view>
				
				
			</view>
			<view>
				
				
				
				<view>
					<view class="enter_item bg5" @tap="url2" data-url="/pages/enter/index">
						<image class="image1" style="margin-top:-1upx;" src="/static/home/invit.png" alt="" mode="widthFix"></image>
						<text class="newTextDesc" style="padding-top:20upx;">渠道</text>
						<image   @click.stop="clickTap" data-index="5" src="/static/addImg/icon_tips@2x.png" style="width:15px;height:15px;z-index:0;"     class="rightImgAb" mode="widthFix"></image>
											
						<view  v-if="this.index==5" class="addNewView">
							对所属渠道的新增,管理,对渠道资料的修改完善,对商户身份,支付方式的修改确认等;
						</view>	
					</view>
				</view>
				<view>
					<view class="enter_item bg7" @tap="url" data-url="/pages/wx/newInvite">
						<image class="image1" style="margin-top:-1upx;" src="/static/addImg/icon_home6.png" alt="" mode="widthFix"></image>
						<text class="newTextDesc" style="padding-top:20upx;">邀请</text>
						<image   @click.stop="clickTap" data-index="6" src="/static/addImg/icon_tips@2x.png" style="width:15px;height:15px;z-index:0;"     class="rightImgAb" mode="widthFix"></image>
											
						<view  v-if="this.index==6" class="addNewView">
							通过二维码邀请下级渠道入驻和直属用户注册乐驿享,建立关联关系,获得渠道收入和交易返佣;
						</view>	
					</view>
				</view>
				
				<view>
					<view class="enter_item bg6" @tap="url" data-url="/pages/msg/msgList">
						<image class="image1" style="margin-top:-1upx;" src="/static/home/msg.png" alt="" mode="widthFix"></image>
						<text class="newTextDesc" style="padding-top:20upx;">消息</text>
						<image   @click.stop="clickTap" data-index="7" src="/static/addImg/icon_tips@2x.png" style="width:15px;height:15px;z-index:0;"     class="rightImgAb" mode="widthFix"></image>
											
						<view  v-if="this.index==7" class="addNewView">
								集中管理关于系统,订单,物流,资金入账的消息通知,方便快捷;
						</view>	
					</view>
				</view>
				
				<view @tap="url" data-url="/pages/system/system">
					<view class="enter_item bg8">
						<image class="image1"  style="margin-top:-1upx;" src="/static/addImg/icon_home8.png" alt="" mode="widthFix"></image>
						<text class="newTextDesc" style="padding-top:20upx;">设置</text>
						<image   @click.stop="clickTap" data-index="8" src="/static/addImg/icon_tips@2x.png" style="width:15px;height:15px;z-index:0;"     class="rightImgAb" mode="widthFix"></image>
											
						<view  v-if="this.index==8" class="addNewView">	
                             处理包括安全手机,登录密码,取现密码,地址管理,清除缓存等系统功能。
						</view>		
					</view>
				</view>
				
			</view>
		</view>
		
		
		<view class="msg" v-if="false">
			<view>
				<image src="/static/home/user.png" alt="" mode="widthFix"></image>
				<view>
					<view class="h5">
						乐享公告
					</view>
					<view>
						【与你有关】春节期间乐享各项工作安排
					</view>
				</view>
			</view>
		</view>
	
	      <view class="botText">
	     			 
				 <view class="botTextInner">
					 <text class="botTextInnerLeft">联系客服</text>
					 <text class="botTextInnerMiddle">
						 <text class="borderText"></text>
						 
					 </text>
					 <text class="botTextInnerRight">常见问题</text>
				 </view>
	     			 
	     </view>
	     		
	
	
	
	
	</view>
</template>

<script>
	export default {
		data() {
			return {
				isPayQR:"",
				shopObj:{},
				showFlag:false,
				marchantId:"",
				textInfo: {},
				index:0,
				invite: "",//13327313408
				isDown: false, //是否显示微信收款等下拉
			}
		},
		methods: {
			myClick:function(e)
			{
				console.log("点击了。。。")
			},
			clickTap:function(e)
			{
				this.showFlag=!this.showFlag;
				this.index=e.currentTarget.dataset.index;
				//e.cancelBubble();
				console.log("你好,你点击的索引是"+this.index);
			},
			limit(limit){
				var size = "";
				size = (limit/(1024 * 1024)).toFixed(2);//转MB
				var sizeStr = size + "";                        //转成字符串
				var index = sizeStr.indexOf(".");                    //获取小数点处的索引
				var dou = sizeStr.substr(index + 1 ,2)            //获取小数点后两位的值
				if(dou == "00"){                                //判断后两位是否为00，如果是则删除00
					return sizeStr.substring(0, index) + sizeStr.substr(index + 3, 2)
				}
				return size;
			},
			//更换店铺图片
			changeImg(){
				let that=this;
				uni.chooseImage({
					count: 1, //默认9
					sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
					success: function (res) {
						if(that.limit(res.tempFiles[0].size)>3){
							uni.showToast({
								title:"图片太大",
								icon:"none"
							})
							return
						}
				        that.$ajax({
							uploadFile:true,
							formData:{
								'fileName':"/marchant/",
							},
							filePath:res.tempFilePaths[0],
							success(d){
								that.uploadImg(d)
								that.shopObj.disPlayImg=d;
								uni.setStorage({
									key:"shopObj",
									data:JSON.stringify(that.shopObj)
								})
							}
						})
						
				
					},
				});
			},
			uploadImg(src){
				let that=this;
				that.$ajax({
					url:"/system_manager/setLogo",
					data:{
						displayImg: src,
						shopId:that.shopObj.shopId
					},success(d){
						console.log(d);
					}
				})
			},
			urlCode(e){
				let type=parseInt(Math.random()*2,10);
				uni.navigateTo({
					url: e.currentTarget.dataset.url+"?type="+type
				})
			},
			url(e) {
				uni.navigateTo({
					url: e.currentTarget.dataset.url
				})
			},
			url2(e)
			{
				let that=this;
				uni.navigateTo({
					url: e.currentTarget.dataset.url+"?merchantId="+that.merchantId
				})
			},
			changeDown(e) {
				this.isDown = !this.isDown
			},
			isExistsOfflinePayQR(){
				let that=this;
				that.$ajax({
					url:"/merchant/isExistsOfflinePayQR",
					data:{
						merchantId:that.shopObj.merchantId
					},
					success(d){
						that.isPayQR=d;
					}
				})
			}
		},
		onShow() {
			let that=this;	
			that.isDown = false;
			that.index=0;
			that.$ajax({
				url:"/token/get",
				method:"POST",
				data:{
					merchantId:that.shopObj.merchantId
				},success(d){
					uni.setStorage({
						key:"Token",
						data:d
					})
					that.$ajax({
						url:"/home/index",
						data:{
							level: that.shopObj.level,
							merchantId: that.shopObj.merchantId,
							shopId: that.shopObj.shopId
						},success(d){		
							that.textInfo=d;
							that.isExistsOfflinePayQR()
						}
					})
				}
			})
		},
		onLoad() {
			let that=this;
			
			uni.getStorage({
				key:"shopObj",
				success(res){
					console.log(res)
					that.shopObj=JSON.parse(res.data);
					that.merchantId=that.shopObj.merchantId;
					console.log("你好,我获取的shopObj是"+that.shopObj)
					console.log("你好,我获取的mechardId是"+that.shopObj.merchantId);
					console.log(that.shopObj)
					if (!that.shopObj.shopId) {
						uni.showModal({
							title: '未登录',
							content: '登录失效，需要登录后才能继续',
							/**
							 * 如果需要强制登录，不显示取消按钮
							 */
							showCancel: !that.forcedLogin,
							success: (res) => {
								if (res.confirm) {
									// /**
									//  * 如果需要强制登录，使用reLaunch方式
									//  */
									if (that.forcedLogin) {
										uni.reLaunch({
											url: '../login/login'
										});
									} else {
										uni.reLaunch({
											url: '../login/login'
										});
									}
								}
							}
						});
					}
				}
			})
		}
	}
</script>

<style scoped>
	* {
		box-sizing: border-box;
	}
	.newTextDesc{
		margin-top:30upx!important;
	}
	
	.addNewView{
      /*  width:260upx; */
		/* height:160upx; */
		padding:6upx 8upx;
		border:1px solid rgba(0,0,0,0.18);
		position:absolute;
		z-index:200;
		font-size:16upx;
		color:rgba(0,0,0,0.66);
		background:#fff;
		/* left:-5px; */
		border-radius:20upx;
		top:-120upx;
	}
	/* .addNewView:nth-of-type(1)
	{
		margin-left:80upx;
	}
	.addNewView:nth-of-type(5)
	{
		margin-left:80upx;
	}
 */
  /*  .addNewView:nth-of-type(4)
	{
		position:relative;
		right:100upx;
	} */
	.botText{
		width:100%;
		height:80upx;
		display:flex;
		align-items:center;
		margin-top:100upx;
		background:#f2f2f2!important;
	}
	
	.botTextInner{
		width:240upx;
		margin:0 auto;
		height:80upx;
		display:block;
		/* flex-direction:row; */
		/* background:green!important; */
	}
	.botTextInnerLeft{
		height:80upx;
		float:left;
		font-size:26upx;
		width:49%;
		text-align:left;
/* 		background: #2ED3B2; */
        line-height:80upx;
		color:rgba(0,0,0,0.86);
	}
	.botTextInnerMiddle{
		width:2%;
		height:80upx;
	}
	.borderText{
		width:1px;
		display:inline-block;
		height:30upx;
		margin-top:25upx;
		background:rgba(0,0,0,0.18)!important;
	}
	.botTextInnerRight{
		height:80upx;
		width:49%;
		line-height:80upx;
		float:right;
		display:block;
/* 		background: #007AFF; */
	    text-align:right; 
       
		font-size:26upx;
		color:rgba(0,0,0,0.86);
		}
	.content {
		padding: 0;
		background: #f2f2f2;
	}

	.img image{
		width:160upx;
		height:160upx;
	}
	.content>view {
		background: #fff;
	}

	.add {
		width: 30upx;
		height: 30upx;
	}

	.system {
		width: 35upx;
		height: 35upx;
	}

	.content .uni-page-head {
		box-sizing: border-box;
		height: 128upx;
		background: rgb(15, 174, 255);
		width: 100%;
		position: fixed;
		top: 0;
		left: 0;
		text-align: center;
		padding: 40upx 30upx 0;
		z-index: 10000;
		color: #fff;
	}

	.uni-page-head .r {
		margin-top: 30upx;
	}
	.uni-page-head .r>view{
		display: inline-block;
		width: 60upx;
	}
	.uni-page-head .r .down {
		background: #fff;
		color: #333;
		position: absolute;
		width: 200upx;
		right: 20upx;
		top: 130upx;
		border-radius: 10upx;
		-webkit-box-shadow: 2upx 2upx #eee;
		box-shadow: 4upx 8upx #eee;
	}

	.uni-page-head .down>view {
		line-height: 80upx;

	}

	.uni-page-head .down .border {
		border-bottom: 1px solid #eee;
	}

	.uni-page-head .up {
		display: block;
		width: 0;
		height: 0;
		border-width: 0px 12upx 16upx;
		border-style: solid;
		border-color: transparent transparent #fff;
		position: absolute;
		top: -16upx;
		left: 100upx;
	}

	.uni-page-head>view {
		display: inline-block;
	}

	.uni-page-head .logo {
		width: 52upx;
		margin-top: 14upx;
		height: 52upx;
	}
	.uni-page-head .center {
		line-height: 58upx;
	}

	.shopInfo {
		margin-top: 128upx;
		padding: 10upx 30upx;
		padding-top: 16upx;
		border-bottom: 1px solid #eee;
	}

	.shopInfo>view {
		display: inline-block;
		vertical-align: top;
		font-size: 28upx;
	}

	.shopInfo image {
		width: 80upx;
		height: 80upx !important;
		margin-right: 20upx;
	}

	.shopInfo .r {
		color: #ee3535;
	}

	.proList {
		padding: 20upx 30upx;
		display: flex;
	}

	.proList>view {
		flex: 1;
		height: 160upx;
		margin-right: 10upx;
	}

	.proList>view image {
		width: 160upx;
		height:160upx;
	}

	.textInfo>view {
		padding: 10upx 30upx;
	}

	.textInfo>view>view {
		width:160upx;
		display: inline-block;
		margin-right: 10upx;
		text-align: center;
	}

	.textInfo .text {
		font-weight: 500;
		color: #333;
		font-size: 26upx;
		margin-top: 20upx;
	}

	.content .banner {
		background: #e2e2e2;
		padding: 20upx 0;
	}

	.banner image {
		width: 100%;
	}

	.enter {
		padding-bottom: 60upx;
	}

	.enter>view {
		display: flex;
	}

	.enter>view>view {
		flex: 1;
		text-align: center;
	}

	.enter .enter_item {
		height: 160upx;
		/* background:red; */
		width: 160upx;
		margin: 36upx auto 0;
		border-radius: 10upx;
		text-align: center;
		position:relative;
	}

	.enter .enter_item .image1 {
		width: 60upx;
		height: 60upx !important;
		margin-top: 20upx;
		position:absolute;
		top:50%;
		margin-top:-30upx;
		left:50%;
		margin-left:-30upx;
	}

	.enter .enter_item text {
		display: block;
		color: #fff;
	}

	.bg1 {
		background: #2ED3B2;
	}

	.bg2 {
		background: #4A9AEE;
	}

	.bg3 {
		background: #E65555;
	}

	.bg4 {
		background: #FFA318;
	}

	.bg5 {
		background: #C458E7;
	}

	.bg6 {
		background: #4ECD72;
	}
	.bg7{
		background:#fA8A47;
	}
	.bg8{
		 background:#4A9AEE;
	}

 


	.content .msg {
		height: 136upx;
		padding-top: 36upx;
		background: #E2E2E2;
	}

	.msg>view {
		height: 100upx;
		background: #fff;
		padding: 0 30upx;

	}

	.msg image {
		width: 72upx;
		height: 72upx;
		margin-top: 14upx;
		margin-right: 22upx;
		background: red;
		vertical-align: middle;
	}

	.msg>view>view {
		display: inline-block;
		font-size: 24upx;
		vertical-align: middle;
	}

	.msg .h5 {
		font-size: 28upx;
	}
		
	.rightImgAb {
		/* width:22px;
		height:22px; */
		position:absolute;
		z-index:300;
		right:10upx;
		top:10upx;	
	}
		
/* 	.rightTextMsg{
		background:red;
		width:400upx;
	} */
</style>
