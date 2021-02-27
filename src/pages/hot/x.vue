<template>
	<view class="index">

		<view class="grid">
			<view class="grid-c-06 mygrid" v-for="item in lists" :key="item.guid">
				<view class="panel myitem" @click="goDetail(item)">
					<image class="view-img " :src="item.img_src"></image>

					<text class="myfont">title</text>
					<text class="myfont font-info">- - info - -</text>
					
					<view class="row view-info">
						<view class="car-title-view row">
							<text class="card-title card-list2-title">￥9999</text>
						</view>


						<view @click.stop="ViewOnClick1(item)" class="card-share-view"></view>
					</view>
				</view>
			</view>
		</view>



		<text class="loadMore">加载...</text>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				refreshing: false,
				lists: [],
				fetchPageNum: 1
			}
		},
		onLoad() {
			this.getData();
		},
		onPullDownRefresh() {
			console.log('下拉刷新');
			this.refreshing = true;
			this.getData();
		},
		onReachBottom() {
			this.getData();
		},
		methods: {
			getData() {
				uni.request({
					url: this.$serverUrl + '/api/picture/posts.php?page=' + (this.refreshing ? 1 : this.fetchPageNum) +
						'	',
					success: (ret) => {
						console.log(ret)
						if (ret.statusCode !== 200) {
							console.log('请求失败:', ret)
						} else {
							if (this.refreshing && ret.data[0].id === this.lists[0].id) {
								uni.showToast({
									title: '已经最新',
									icon: 'none',
								});
								this.refreshing = false;
								uni.stopPullDownRefresh();
								return;
							}
							let list = [],
								data = ret.data;
							for (let i = 0, length = data.length; i < length; i++) {
								var item = data[i];
								item.guid = this.newGuid() + item.id
								list.push(item);
							}
							console.log('得到list', list);
							if (this.refreshing) {
								this.refreshing = false;
								uni.stopPullDownRefresh()
								this.lists = list;
								this.fetchPageNum = 2;
							} else {
								this.lists = this.lists.concat(list);
								this.fetchPageNum += 1;
							}
						}
					}
				});
			},
			newGuid() {
				let s4 = function() {
					return (65536 * (1 + Math.random()) | 0).toString(16).substring(1);
				}
				return (s4() + s4() + "-" + s4() + "-4" + s4().substr(0, 3) + "-" + s4() + "-" + s4() + s4() + s4()).toUpperCase();
			},
			goDetail(e) {
				uni.navigateTo({
					url: '../detail/detail?data=' + encodeURIComponent(JSON.stringify(e))
				})
			},

			ViewOnClick1(e) {
				
			}
		}
	}
</script>

<style>
	.grid{
		padding-top: 10px;
	}
	.mygrid{
		margin-top: 5px;
	}
	.myitem{
		height: 45vh;
		border-radius:25px;
	}

	.view-img {
	width: 345upx;
	height: 30vh;
	}
	.view-info {
		background-color: #ff7ae250;
		align-items: center;
		justify-content: center;
	}
	.myfont {
	flex: 1;
	font-weight:bold;
	font-size: 26upx;
	text-align: left;
	color: #000000;
	text-overflow: ellipsis;
	display: -webkit-box;
	white-space: normal;
	display: -webkit-box;
	-webkit-box-orient: vertical;
	-webkit-line-clamp: 2;
	overflow: hidden;

	margin-left: 15upx ;

	}

	.font-info {
	font-size: 24upx;
	color: #707070;
	font-weight: normal;
	}
</style>
