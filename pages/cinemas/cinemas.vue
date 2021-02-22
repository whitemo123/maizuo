<template>
	<view class="content">
		<view class="status_bar"></view>
		<view class="header">
			<view class="city">上海<image src="../../static/imgs/down.png"></image></view>
			<view class="title">影院</view>
			<view class="search">
				<image @tap="search" src="../../static/imgs/search.png"></image>
			</view>
		</view>
		<view class="film-list">
			<cinema-item :cinemaList="cinemaList"></cinema-item>
		</view>
	</view>
</template>

<script>
	import cinemaItem from '../../components/cinema-item.vue'
	
	export default {
		components: {
			"cinema-item": cinemaItem,
		},
		data() {
			return {
				cinemaList: [],
			}
		},
		onLoad() {
			let that = this;
			uni.request({
				url: `http://192.168.31.183:3000/cinema?id=310100`,
				method:'GET',
				success(e) {
					that.cinemaList = e.data;
				}
			})
		},
		methods: {
			search() {
				uni.navigateTo({
					url: '../search/search',
					animationType: 'pop-in',
					animationDuration: 200
				})
			}
		}
	}
</script>

<style>
	uni-page-body {
		height: 100%;
	}
	.content {
		height: 100%;
		display: flex;
		flex-direction: column;
	}
	.status_bar {
		width: 100vw;
		height: var(--status-bar-height);
		background-color: #FFFFFF;
	}
	.header {
		width: 100vw;
		height: 44px;
		background-color: #fff;
		padding: 0 30rpx;
		box-sizing: border-box;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.header .city {
		flex: 1.5;
		display: flex;
		justify-content: left;
		align-items: center;
		color: #191a1b;
		font-size: 26rpx;
	}
	.header .city image {
		width: 24rpx;
		height: 12rpx;
		margin-left: 10rpx;
	}
	.header .title {
		flex: 6;
		display: flex;
		justify-content: center;
		align-items: center;
		color: #191a1b;
		font-size: 34rpx;
	}
	.header .search {
		flex: 1.5;
		height: 44px;
		display: flex;
		justify-content: flex-end;
		align-items: center;
	}
	.header .search image {
		width: 36rpx;
		height: 36rpx;
	}
	.film-list {
		width: 100vw;
		height: calc(100% - 44px);
		overflow: scroll;
	}
	.film-item {
		width: 100%;
		padding: 30rpx;
		background-color: #FFFFFF;
		display: flex;
		justify-content: center;
		align-items: center;
		border-top: 1px solid #ededed;
	}
	.film-info-lf {
		flex: 7;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: left;
	}
	.film-info-lf text:nth-child(1) {
		color: #191a1b;
		font-size: 30rpx;
		max-width: 80%;
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
	}
	.film-info-lf text:nth-child(2) {
		color: #797d82;
		font-size: 24rpx;
		margin-top: 10rpx;
		max-width: 80%;
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
	}
	.film-info-rt {
		flex: 3;
		display: flex;
		flex-direction: column;
		align-items: flex-end;
		justify-content: center;
	}
	.film-info-rt>text {
		color: #797d82;
		font-size: 22rpx;
		margin-top: 10rpx;
		font-weight: 400;
	}
	.film-info-rt .price {
		color: #ff5f16;
		font-size: 22rpx;
	}
	.film-info-rt .price text {
		font-size: 30rpx;
	}
</style>
