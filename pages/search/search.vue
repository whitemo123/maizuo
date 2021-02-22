<template>
	<view class="content">
		<view class="status_bar"></view>
		<view class="cu-bar bg-white search">
			<view class="search-form radius">
				<text class="cuIcon-search"></text>
				<input v-model="keywords" :adjust-position="false" type="text" placeholder="输入影城名称" confirm-type="search"></input>
			</view>
			<view class="action">
				<text @tap="clear" class="cuIcon-close"></text>
				<text @tap="back">取消</text>
			</view>
		</view>
		<view class="main">
			<view v-if="!keywords" class="recent">
				<text>离你最近</text>
				<view class="recent-list">
					<text>橙天嘉禾影城（五彩城店）</text>
					<text>上海枫泾天娱影城</text>
					<text>博万国际影城（青浦朱家角店）</text>
				</view>
			</view>
			<view v-else class="search-list">
				<cinema-item :cinemaList="cinemaList"></cinema-item>
			</view>
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
				keywords: '',
				cinemaList: [],
			}
		},
		methods: {
			back() {
				uni.navigateBack({
					animationType:'fade-out',
					animationDuration:200
				})
			},
			clear() {
				this.keywords = '';
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
	.main {
		width: 100vw;
		height: calc(100% - 50px);
		background-color: #FFFFFF;
		overflow: scroll;
	}
	.recent {
		width: 100vw;
		padding: 0 30rpx 16rpx;
	}
	.recent>text {
		display: block;
		font-size: 26rpx;
		color: #bdc0c5;
		margin: 36rpx 0;
	}
	.recent-list {
		width: 100%;
		display: flex;
		flex-wrap: wrap;
		border-bottom: 1px solid #ededed;
		padding-bottom: 20rpx;
	}
	.recent-list text {
		display: block;
		background-color: hsla(0,0%,95.7%,.6);
		height: 60rpx;
		line-height: 28rpx;
		border-radius: 6rpx;
		font-size: 26rpx;
		padding: 16rpx 24rpx;
		text-align: center;
		box-sizing: border-box;
		margin: 10rpx;
	}
</style>
