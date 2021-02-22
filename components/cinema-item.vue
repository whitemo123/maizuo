<template>
	<view>
		<view v-for="value in cinemaList" :key="value.cinemaId" class="film-item">
			<view class="film-info-lf">
				<text>{{ value.name }}</text>
				<text>{{ value.address }}</text>
			</view>
			<view class="film-info-rt">
				<view class="price">￥<text>{{ value.lowPrice | priceFilter }}</text>起</view>
				<text>803.5km</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			cinemaList: {
				type: Array,
				required: true,
			}
		},
		filters: {
			priceFilter(num) {
				return num / 100;
			}
		}
	}
</script>

<style>
	.film-item {
		width: 100%;
		padding: 30rpx;
		background-color: #FFFFFF;
		display: flex;
		justify-content: center;
		align-items: center;
		border-top: 1px solid #ededed;
		overflow: hidden;
	}
	.film-info-lf {
		flex: 8;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: left;
		overflow: hidden;
	}
	.film-info-lf text:nth-child(1) {
		color: #191a1b;
		font-size: 30rpx;
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
	}
	.film-info-lf text:nth-child(2) {
		color: #797d82;
		font-size: 24rpx;
		margin-top: 10rpx;
		max-width: 95%;
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
	}
	.film-info-rt {
		flex: 2;
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
