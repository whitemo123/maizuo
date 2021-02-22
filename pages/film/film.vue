<template>
	<view class="content">
		<view class="status_bar"></view>
		<view class="header"><image @tap="back" src="../../static/imgs/back.png"></image></view>
		<view class="cover">
			<image class="cover-img" :src="cover" mode="center"></image>
			<view class="fim-detail">
				<view class="title">
					<view class="name">你好，李焕英<text>2D</text></view>
					<view class="grade"><text>7.4</text>分</view>
				</view>
				<view class="detail">喜剧 | 剧情</view>
				<view class="time"><text>2021-02-21</text>上映</view>
				<view class="info"><text>中国大陆</text>|<text>128</text>分钟</view>
				<view class="desc" :class="isDown?'active':''">2001年的某一天，刚刚考上大学的贾晓玲（贾玲 饰）经历了人生中的一次大起大落。一心想要成为母亲骄傲的她却因母亲突遭严重意外，而悲痛万分。在贾晓玲情绪崩溃的状态下，竟意外的回到了 1981 年，并与年轻的母亲李焕英（张小斐 饰）相遇，二人形影不离，宛如闺蜜。与此同时，也结识了一群天真善良的好朋友。晓玲以为来到了这片“广阔天地”，她可以凭借自己超前的思维，让母亲“大有作为”，但结果却让晓玲感到意外......</view>
				<view class="more" :class="isDown?'down':''" @tap="down"><image src="../../static/imgs/down.png"></image></view>
			</view>
		</view>
		<view class="author-box">
			<text>演职人员</text>
			<swiper :display-multiple-items="4">
				<swiper-item v-for="index in 5" :key="index">
					<view class="author-item">
						<image mode="aspectFill" src="https://pic.maizuo.com/usr/movie/577c7d72a1908638a805b4be88aeb791.jpg?x-oss-process=image/quality,Q_70"></image>
						<text>贾玲</text>
						<text>导演</text>
					</view>
				</swiper-item>
			</swiper>
		</view>
		<view class="photos">
			<text>剧照</text>
			<swiper :display-multiple-items="3" previous-margin="30rpx" next-margin="30rpx">
				<swiper-item v-for="index in 5" :key="index">
					<view class="photo-item">
						<image mode="aspectFill" src="https://pic.maizuo.com/usr/2021/0d1064c76b021e476832ec2f469d4bbe.jpg?x-oss-process=image/quality,Q_70"></image>
					</view>
				</swiper-item>
			</swiper>
		</view>
		<button class="btn">选座购票</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				isDown: false,
				cover: 'https://pic.maizuo.com/usr/movie/962152780002ba0925aabe6bed25576f.jpg?x-oss-process=image/quality,Q_70',
			}
		},
		onLoad(options) {
			const id = options.id;
		},
		methods: {
			back() {
				uni.navigateBack({
					animationType: 'pop-out',
					animationDuration: 200
				});
			},
			down() {
				console.log("牛逼");
				this.isDown = !this.isDown;
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
	}
	.cover {
		width: 100vw;
		background-size: 100%;
		background-position: 0% 120%;
	}
	.cover-img {
		width: 100vw;
		height: 420rpx;
	}
	.header {
		width: 100vw;
		height: 88rpx;
		text-align: left;
		position: absolute;
		top: var(--status-bar-height);
		left: 0;
		z-index: 99;
	}
	.header image {
		width: 60rpx;
		height: 60rpx;
		margin-left: 10rpx;
		margin-top: 10rpx;
	}
	.fim-detail {
		width: 100vw;
		background-color: #FFFFFF;
		box-sizing: border-box;
		padding: 24rpx 30rpx;
	}
	.fim-detail .title {
		width: 100%;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
	.fim-detail .title .name {
		color: #191a1b;
		font-size: 36rpx;
		height: 48rpx;
		line-height: 48rpx;
		display: flex;
		align-items: center;
	}
	.fim-detail .title .grade {
		color: #ffb232;
		font-size: 20rpx;
		font-style: normal;
	}
	.fim-detail .title .grade text {
		font-size: 36rpx;
		font-style: italic;
	}
	.fim-detail .title .name text {
		display: inline-block;
		color: #FFFFFF;
		background-color: #d2d6dc;
		height: 28rpx;
		line-height: 28rpx;
		padding: 0 4rpx;
		border-radius: 4rpx;
		font-size: 18rpx;
		margin-left: 14rpx;
	}
	.fim-detail .detail, .fim-detail .time, .fim-detail .info, .fim-detail .desc {
		color: #797d82;
		font-size: 26rpx;
		margin-top: 8rpx;
	}
	.fim-detail .info text:nth-child(1) {
		margin-right: 10rpx;
	}
	.fim-detail .info text:nth-child(2) {
		margin-left: 10rpx;
	}
	.fim-detail .desc {
		width: 100%;
		height: 76rpx;
		margin-top: 24rpx;
		overflow: hidden;
	}
	.fim-detail .active {
		height: auto;
	}
	.fim-detail .more {
		width: 100%;
		height: 60rpx;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.fim-detail .more image {
		width: 16rpx;
		height: 8rpx;
	}
	.fim-detail .down {
		transform: rotate(180deg);
	}
	.author-box {
		width: 100vw;
		background-color: #FFFFFF;
		margin-top: 20rpx;
	}
	.author-box>text {
		display: block;
		width: 100%;
		color: #191a1b;
		font-size: 32rpx;
		padding: 30rpx;
	}
	.author-box swiper {
		width: 100%;
		height: 280rpx;
	}
	.author-box swiper swiper-item {
		width: 170rpx;
	}
	.author-box .author-item {
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
	}
	.author-box .author-item image {
		width: 170rpx;
		height: 170rpx;
	}
	.author-box .author-item text:nth-child(2) {
		color: #191a1b;
		font-size: 24rpx;
		margin-top: 20rpx;
		height: 36rpx;
	}
	.author-box .author-item text:nth-child(3) {
		color: #797d82;
		font-size: 20rpx;
	}
	.photos {
		width: 100vw;
		background-color: #FFFFFF;
		margin-top: 20rpx;
		margin-bottom: 120rpx;
	}
	.photos>text {
		color: #191a1b;
		font-size: 32rpx;
		display: block;
		padding: 30rpx;
	}
	.photos image {
		width: 300rpx;
		height: 200rpx;
	}
	.btn {
		width: 100vw;
		height: 98rpx;
		background-color: #ff5f16;
		font-size: 32rpx;
		line-height: 98rpx;
		position: fixed;
		bottom: 0;
		left: 0;
		border-radius: 0;
		color: #fff;
	}
</style>
