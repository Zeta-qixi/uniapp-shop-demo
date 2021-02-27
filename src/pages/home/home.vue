<template>
	
<view class="zindex">
	<view class="page">
		<swiper class="swiper" autoplay="true">
			<swiper-item v-for="item in testdata" :key="item.id">
				<image style="width:100%;" :src="item.img" will-change= "transform" @click="goAd(item.id)"></image>
			</swiper-item>
		</swiper>
    </view>

	<view class="search-box">
	<view style="background-color:#00000020;width:10%;"></view>
	<text style="width:45%;color:#00000070;margin:auto 0 auto 10rpx;font-size:30rpx;">{{shopName}}</text>
	<view style="background-color:#00000020;width:10%;" @click.stop="goMap"></view>
	<view style="background-color:#00000040;width:10%;" @click.stop="goTelePhone"></view>
	<view style="background-color:red;width:25%;color=#00ffff;border-radius:0 20rpx 20rpx 0;">
	<text style="text-align:center;color:#fff;font-size:30rpx;margin:auto;" @click.stop="goShopList">切换门店</text>
	</view>
	</view>

	<view class="box">
		<view class="box-item" @click="buttonBox" id="A"><button>A</button></view>
		<view class="box-item" @click="buttonBox" id="B"><button>B</button></view>
		<view class="box-item box-end-item" @click="buttonBox" id="C"><button>C</button></view>
	</view>

	<view class='box2'>
			<view class="text">新品推荐</view>
			<view class="more">更多 ></view>
	</view>
	<product-list style="max-height:0;"></product-list>
	

</view>

</template>



<script>

import sortdata from '../../data/imagedata.json'
export default {

    data() {
        return {
			testdata: sortdata.lists,
			shopName: '请手动定位...'
        }
    },
	methods:{
			buttonBox(e){
				let id = e.currentTarget.id
				//--跳转到相应页面
				switch(id){
					case 'A': 
					console.log(e.currentTarget.id)
					break
					case 'B': 
					console.log(e.currentTarget.id)
					break
					case 'C': 
					console.log(e.currentTarget.id)
					break
					default: break;
				}
				
			},
			goShopList(e){
				let _vm=this
				uni.navigateTo(
				
				{
				url: '../shoplist/shoplist',
				events:{
					acceptDataFromOpenedPage0: function(data){
						_vm.shopName=data.shopname
					}
				},
				success: function(res){
					res.eventChannel.emit('acceptData1',{sentdata:'1'})
				},
				})
				
				
			},
			goTelePhone(e){
				//调用电话api
				console.log("telephone")
			},
			goMap(e){
				//调用地图api
				console.log("map")
			},
			goAd(e){
				//轮播图页面跳转
				console.log(e)
			}
			

		}

}
</script>

<style>

.zindex {
	display: inline-block;
	vertical-align:top;
	width: 750upx;
	min-height: 100vh;
	flex-direction: column;
}
.page {
	width: 100%;
	height: 30%;
}
.swiper {
	height: 100%;
	flex: 1;
	background-color: #000000;
	
}
	
.box{
	width: auto;
	padding: 5% 2% 0 2%;
	height: 20%;
	flex-direction: row;
	background-color: rgb(255, 255, 255);
}
.box-item{
	border-right: 4rpx rgba(7, 7, 7, 0.1) solid;
	flex: 1;
	width: 30%;
	
	margin: 10rpx 0rpx 10rpx 0rpx;
	
}
.box-end-item{
	border-right: 0;
}
.box button{
	margin: auto 10% auto 10%;
	height: 85%;
	background-color: #ffffff10;
	box-shadow: 3rpx 5rpx 4rpx 3rpx rgba(0, 0, 0,0.3);	
}

.search-box{
	box-shadow: 3rpx 5rpx 4rpx 4rpx rgba(0, 0, 0,0.3);
 
	border-radius:20rpx;
	left: 3%;
	top: 27%;
	height: 5%;
	width: 90%;
	position: absolute;
	background-color: white;
	padding: 0 0 0 15rpx;
	flex-direction: row;
	
}

.box2{
	margin: 10rpx 30rpx;
	flex-direction: column;
}
.box2 .text{
	border-left: 5rpx rgb(255, 0, 0) solid;
	padding-left: 10rpx;
	margin-left: 10rpx;
	font: bolder;
	font-size: 32rpx;

}
.box2 .more{
	margin-right: 20rpx;
	font-size: 28rpx;
	position: absolute;
	right: 20rpx;
	color: rgba(0, 0, 0, 0.5);
}


</style>


