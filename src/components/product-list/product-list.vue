<template>
    <view class="game-list">
        <view class="grid-c-06 grid_" v-for="item in lists" :key="item.id">
            <view class="panel panel_" @click="goDetail(item)">
                <image class="img" :src="item.img_src"></image>
                <text class="font">title</text>
                <text class="font font-info">- - info - -</text>
				<view class="price-tag">
					<text class="price">￥9999</text>
					<view class="add-icon" @click.stop="addProduct(item)">+</view>
					<view class="buy-button" @click.stop="goBuy(item)">立即购买</view>
				</view>
            </view>
        </view>
    </view>
</template>


<script>
import productdata from '../../data/productlist.json'
	export default {
		data() {
			return {
				refreshing: false,
				lists:productdata.lists
			}
		},
        methods: {

			addProduct(e){
				console.log("加购:"+e.id)
			},
			goBuy(e){
				console.log("buy:"+e.id)
			},
			goDetail(e) {
				uni.navigateTo({
					url: '../detail/detail?data=' + encodeURIComponent(JSON.stringify(e))
				})
			},
        }
		
	}
</script>

<style>

.panel_{
    height: 40vh;
    border-radius:20rpx;
}
.game-list{
    box-sizing: border-box;
    display: flex;
    flex-direction: row;
	flex-wrap: wrap;
    overflow: auto;
	margin: 10rpx 15rpx 0 15rpx;
	
}
.grid_{
    padding-top: 10px;
}
.img{
    height: 66%;
    width: 45vw;
	border-radius: 10upx;
	
	flex-direction: column;
	background-color: #b9b9b9;

}

.panel_ .font {
	flex: 1;
	font-weight:bold;
	font-size: 28rpx;
	color: #000000;
	text-overflow: ellipsis;
	overflow: hidden;   
	margin-left: 15rpx ;

}

.panel_ .font-info {
	font-size: 26rpx;
	color: #707070;
	font-weight: normal;
    
}
.price-tag {
	
	flex-direction: row; 
    align-items:center;
    justify-content: flex-start;
    margin-bottom: 15rpx;

}
.price{
	font-weight:bold;
    font-size: 32rpx;
	color: #ff0000;
	overflow: hidden;
	max-width: 40%;
}
.add-icon{
	border-radius:100%;
	background-color: #ff0000;
	
	width: 40rpx;	
	height: 40rpx;
	font-weight:bold;
	font-size: 30rpx;
	align-items: center;
	justify-content: center;
	color: #ffffff;
	margin-left: 10%;
}

.buy-button{
	 border-radius:10rpx;
	background-color: #ff0000;
	color: #ffffff;
	width: 40%;	
	height: 50rpx;
	font-size: 26rpx;
	align-items: center;
	justify-content: center;
	margin-left: 10rpx;
}
</style>
