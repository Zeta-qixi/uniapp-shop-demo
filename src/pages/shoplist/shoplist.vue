<template>
    <view class="shop-list">
        <view class="grid_" v-for="item in shoplist" :key="item.id">
            <view class="panel_" @click="chooseShop(item)">
                <view class="image-box">
                <image class="icon"></image>
                </view>
                <view class="text-box">
                    <text class="font">{{item.name}}</text>
                    <text class="font font-info">{{item.info}}</text>
                </view>
                 
                <view class="image-box" >
                    <view  class="button-box" @click.stop="goMap"></view>
                <!--
                    <image style="flex: 2;height: 60%; width:60%;" src="../../static/image/goto.png"></image>
                    <text class = "font">3.3km</text>
                -->
                </view>
                
            </view>
        </view>
    </view>
</template>

<script>
import sortdata from '../../data/shoplist.json'
    export default{
        data(){
            return{
                shoplist: sortdata.lists,
                data:null,
                eventChannel:null
            };
        },
        onLoad: function(e){

            this.eventChannel = this.getOpenerEventChannel()
            this.eventChannel.on('acceptData1', function(data) {
            this.data = data
            })
        },
        onUnload() {
            this.eventChannel.off('acceptData1')
        },
        methods: {
            chooseShop(shop) { 
                this.eventChannel.emit('acceptDataFromOpenedPage0',{shopname:shop.name})
            uni.navigateBack({
                delta: 1
            });            
            },

            goMap(e){
                console.log('调用wx地图api')
            }
        }
    }
</script>

<style>
.shop-list{
    flex: 1;
	width: 100vw;
	min-height: 100vh;
	flex-direction: column;
    margin: 0 20rpx 0 20rpx;
}

.grid_{
    width: 100%;
    flex-direction: column; 
    flex: 0 0 auto;
}

.panel_{
    width: 100%;
    flex-direction: row;
    height: 13vh;
    border-radius:20rpx;
    background-color: rgb(255, 255, 255);
    margin-top: 30rpx;
}

.text-box{
    width: 60%;
    flex-direction: column;
    justify-content: center;
    padding-left: 15rpx;
}

.text-box .font {
	font-weight:bold;
	font-size: 32rpx;
	color: #000000;
	overflow: hidden;   
    text-overflow: ellipsis;
	margin: 0 15rpx 5rpx 15rpx;
}

.text-box .font-info {
    max-height: 45%;
    font-weight: normal;
	font-size: 20rpx;
	color: #707070;
}

.image-box{
    border-radius:20rpx;
    height: 100%;
    width: 20%;
    justify-content: center;
    align-items: center;
}

.image-box .button-box{
    height: 100rpx; 
    width:100rpx; 
    background-color: rgba(0, 0, 0, 0.05);
    border-radius:10rpx;
}

.image-box .icon{
    height: 120rpx; 
    width:120rpx; 
    background-color: rgb(0, 0, 0);
    border-radius:100%;
    margin-left: 20rpx;
}

.image-box .font{
    font-size: 26rpx;
	color: #707070;
    flex: 1;
}
</style>
