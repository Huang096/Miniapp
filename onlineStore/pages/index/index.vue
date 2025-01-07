<template>
	<view class="content">
		<swiper class="swiper-container" indicator-dots="true" autoplay="true" interval="3000" duration="500">
			<swiper-item>
				<image src="/static/image1.png" class="slide-image"></image>
			</swiper-item>
			<swiper-item>
				<image src="/static/image2.png" class="slide-image"></image>
			</swiper-item>
			<swiper-item>
				<image src="/static/image3.png" class="slide-image"></image>
			</swiper-item>
		</swiper>
		<view class="text-area">
			<text class="title">{{title}}</text>
		</view>
	</view>
</template>


<script>
	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.swiper-container {
		width: 750rpx; /* 取决于你的设计需求 */
		height: 400rpx; /* 轮播图的高度，根据需要调整 */
		margin-top: 50rpx; /* 顶部边距 */
	}

	.slide-image {
		width: 100%; /* 让图片充满swiper-item */
		height: 100%; /* 根据swiper-container的高度自动调整 */
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>

