<template>
	<view class="content">
		<view class="status_bar"></view>
		<view class="banner">
			<swiper autoplay="true" circular="true">
				<swiper-item v-for="value in bannerList" :key="value.name">
					<img :src="value.pic">
				</swiper-item>
			</swiper>
		</view>
		<view class="main">
			<scroll-view scroll-x class="bg-white nav">
				<view class="flex text-center">
					<view class="cu-item flex-sub" :class="index==tabIndex?'text-orange cur':''" v-for="(item,index) in tabList" :key="index" @tap="tabSelected" :data-id="index">
						{{ item }}
					</view>
				</view>
			</scroll-view>
			<view class="cu-load loading" v-if="movieList.length==0"></view>
			<view v-for="value in movieList" :key="value.id" class="movieitem" @click="navToFilm(value.id)">
				<view class="movie-pic"><image :src="value.pic"/></view>
				<view class="movie-detail">
					<view class="title">{{ value.name }}<text>{{ value.type }}</text></view>
					<view class="grade">观众评分 <text>{{ value.grade }}</text></view>
					<view class="author">主演：{{ value.actors }}</view>
					<view class="info"><text>{{ value.nation }}</text>|<text>110分钟</text></view>
				</view>
				<view class="movie-btn"><text @click.native.top="shop">购票</text></view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				tabIndex: 0,
				tabList: ['正在热映', '即将上映'],
				movieList: [],
				bannerList: [],
			}
		},
		onLoad() {
			console.log("第一次加载");
			this.getBannerList(310100);
			this.getMovieList(310100, 1, 1);
		},
		methods: {
			tabSelected(e) {
				this.movieList = [];
				this.tabIndex = e.currentTarget.dataset.id;
				this.getMovieList(310100, parseInt(this.tabIndex) + 1, 1);
			},
			navToFilm(id) {
				uni.navigateTo({
					url: '../film/film?id='+id,
					animationType: 'pop-in',
					animationDuration: 200
				})
				
			},
			shop() {
				console.log("购票");
			},
			getBannerList(id) {
				let that = this;
				uni.request({
					url:`http://192.168.31.183:3000/banner?id=${id}`,
					method:'GET',
					success(e) {
						that.bannerList = e.data;
					}
				})
			},
			getMovieList(id,type,page) {
				let that = this;
				uni.request({
					url:`http://192.168.31.183:3000/film?id=${id}&page=${page}&type=${type}`,
					method:'GET',
					success(e) {
						that.movieList = e.data;
					}
				})
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
	}
	.status_bar {
		width: 100vw;
		height: var(--status-bar-height);
		background-color: #FFFFFF;
		position: sticky;
		top: 0;
	}
	.banner {
		width: 100vw;
		height: 25vh;
		background-color: red;
	}
	.banner swiper, swiper img {
		width: 100%;
		height: inherit;
	}
	.main {
		width: 100vw;
		height: calc(75% - 50);
	}
	.text-orange {
		color: #ff5f16;
	}
	.bg-white {
		color: #191a1b;
	}
	.nav {
		position: sticky;
		top: var(--status-bar-height);
		z-index: 99;
	}
	.movieitem {
		width: 100%;
		height: 226rpx;
		padding: 27rpx;
		box-sizing: border-box;
		background-color: #fff;
		border-bottom: 1px solid #ededed;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.movie-pic {
		flex: 2;
		height: 188rpx;
		border-radius: 4rpx;
	}
	.movie-detail {
		flex: 6.5;
		padding-left: 10px;
		overflow: hidden;
	}
	.movie-pic image {
		width: 132rpx;
		height: 188rpx;
		border-radius: 4rpx;
	}
	.movie-btn {
		flex: 1.5;
	}
	.movie-btn text {
		display: block;
		width: 100%;
		height: 50rpx;
		color: #ff5f16;
		font-size: 26rpx;
		text-align: center;
		line-height: 50rpx;
		border: 1px solid #ff5f16;
		border-radius: 4px;
	}
	.movie-detail .title {
		color: #191a1b;
		font-size: 32rpx;
		height: 28rpx;
		width: 100%;
		line-height: 28rpx;
		display: flex;
		align-items: center;
	}
	.movie-detail .title text {
		display: inline-block;
		color: #fff;
		background-color: #d2d6dc;
		font-size: 18rpx;
		height: 28rpx;
		line-height: 28rpx;
		margin-left: 5px;
		padding: 0 4rpx;
		box-sizing: border-box;
	}
	.movie-detail .grade {
		width: 100%;
		color: #797d82;
		font-size: 26rpx;
		margin-top: 10rpx;
	}
	.movie-detail .grade text {
		color: #ffb232;
		font-size: 28rpx;
		margin-left: 10rpx;
	}
	.movie-detail .author, .movie-detail .info {
		width: 100%;
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
		color: #797d82;
		margin-top: 8rpx;
		font-size: 26rpx;
	}
	.movie-detail .info text:nth-child(1) {
		margin-right: 10rpx;
	}
	.movie-detail .info text:nth-child(2) {
		margin-left: 10rpx;
	}
</style>
