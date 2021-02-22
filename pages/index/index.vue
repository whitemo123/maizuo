<template>
	<view class="content">
		<view class="status_bar"></view>
		<view class="banner">
			<swiper autoplay="true" circular="true">
				<swiper-item>
					<img src="https://static.maizuo.com/v5/upload/189bcf606b4bf49ad5de201a2ea5024d.jpg?x-oss-process=image/quality,Q_70">
				</swiper-item>
				<swiper-item>
					<img src="https://static.maizuo.com/v5/upload/189bcf606b4bf49ad5de201a2ea5024d.jpg?x-oss-process=image/quality,Q_70">
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
			<view v-for="index in 10" :key="index" class="movieitem" @click="navToFilm(index)">
				<view class="movie-pic"><image src="https://pic.maizuo.com/usr/movie/3f97c0ef0eca443b9307fad1c05c188e.jpg?x-oss-process=image/quality,Q_70"/></view>
				<view class="movie-detail">
					<view class="title">你好，李焕英<text>2D</text></view>
					<view class="grade">观众评分 <text>7.4</text></view>
					<view class="author">主演：<text>贾玲 张小斐 沈腾 陈赫</text></view>
					<view class="info"><text>中国大陆</text>|<text>110分钟</text></view>
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
				movieList: []
			}
		},
		onLoad() {
			console.log("第一次加载");
		},
		methods: {
			tabSelected(e) {
				this.tabIndex = e.currentTarget.dataset.id;
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
