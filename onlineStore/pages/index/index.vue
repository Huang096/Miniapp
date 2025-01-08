<template>
	<view class="content">
		<swiper class="swiper-container" indicator-dots="true" autoplay="true" interval="3000" duration="500">
			<swiper-item>
				<image src="/static/img/rotate1.jpg" class="slide-image"></image>
			</swiper-item>
			<swiper-item>
				<image src="/static/img/rotate2.jpg" class="slide-image"></image>
			</swiper-item>
			<swiper-item>
				<image src="/static/img/rotate3.jpg" class="slide-image"></image>
			</swiper-item>
		</swiper>

		<view class="search-container">
			<icon type="search" size="20" class="search-icon"></icon>
			<input class="search-bar" type="text" placeholder="请输入关键词"/>
		</view>

		<view class="icon-row">
			<view class="icon-container" v-for="(item, index) in icons" :key="index">
				<view class="icon-image">
					<image :src="item.imgSrc" mode="aspectFill"></image>
				</view>
				<text class="icon-text">{{item.text}}</text>
			</view>
		</view>

		<view class="hotspot-text">
            近期热点
        </view>

		<view class="hotspot-items">
			<view class="hotspot-item" v-for="(item, index) in hotspotItems" :key="index">
				<image :src="item.imgSrc" mode="widthFix" class="item-image"></image>
				<view class="item-info">
				<text class="item-title">{{ item.title }}</text>
				<text class="item-description">{{ item.description }}</text>
				</view>
			</view>
		</view>



		<view class="navbar">
			<view class="nav-item" v-for="(item, index) in navbarItems" :key="index" @click="onNavClick(index)">
				<i :class="item.icon" class="nav-icon"></i>
				<text class="nav-text">{{ item.text }}</text>
			</view>
		</view>
	</view>
</template>


<script>
	export default {
		data() {
			return {
				icons: [
					{ imgSrc: "/static/img/icon1.jpg", text: "图标一" },
					{ imgSrc: "/static/img/icon2.jpg", text: "图标二" },
					{ imgSrc: "/static/img/icon3.jpg", text: "图标三" },
					{ imgSrc: "/static/img/icon4.jpg", text: "图标四" }
				],
				navbarItems: [
					{ icon: 'fa fa-home', text: '首页' },
					{ icon: 'fa fa-th', text: '分类' },
					{ icon: 'fa fa-shopping-cart', text: '购物车' },
					{ icon: 'fa fa-user', text: '我的' }
				],
				hotspotItems: [
					{
						imgSrc: "/static/img/product1.jpg",
						title: "商品标题1",
						description: "描述信息1"
					},
					{
						imgSrc: "/static/img/product2.jpg",
						title: "商品标题2",
						description: "描述信息2"
					},
					{
						imgSrc: "/static/img/product2.jpg",
						title: "商品标题2",
						description: "描述信息2"
					},
					{
						imgSrc: "/static/img/product1.jpg",
						title: "商品标题1",
						description: "描述信息1"
					},
				]
			}
		},
		onLoad() {

		},
		methods: {
			onNavClick(index) {
				console.log('导航项被点击:', index);
				// 根据index来切换页面或做其他操作
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		width: 100%;
		overflow: hidden;
	}

	.swiper-container {
		width: 750rpx; /* 取决于你的设计需求 */
		height: 400rpx; /* 轮播图的高度，根据需要调整 */
		margin-top: 0rpx; /* 顶部边距 */
	}

	.slide-image {
		width: 100%; /* 让图片充满swiper-item */
		height: 100%; /* 根据swiper-container的高度自动调整 */
		object-fit: cover;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}

	.search-container {
		position: relative;
		width: 100%;
		box-sizing: border-box;
		display: flex;
		justify-content: center;
		padding: 20rpx;
	}

	.search-bar {
		width: 100%;
		height: 60rpx; /* 高度可调 */
		border: 1rpx solid #ccc; /* 边框颜色和宽度 */
		border-radius: 40rpx; /* 圆角大小 */
		padding-left: 80rpx;
		font-size: 28rpx; /* 文字大小 */
		background-color:#f2f2f2;;
	}

	.search-icon {
		position: absolute;
		left: 40rpx; /* Adjust this value to align the icon as needed */
		top: 50%;
		transform: translateY(-50%);
		color: #ccc;
	}

	.search-bar::placeholder {
    color: #aaa; /* 调整placeholder文字的颜色 */
	}

	.icon-row {
		display: flex;
		justify-content: space-around;
		width: 100%;
		margin-top: 20rpx;
	}

	.icon-container {
		display: flex;
		flex-direction: column;
		align-items: center;
		width: 150rpx; /* 根据需求调整 */
	}

	.icon-image {
		width: 100rpx;
		height: 100rpx;
		border-radius: 50%; /* 使图片呈圆形 */
		overflow: hidden;
	}

	.icon-image image {
		width: 100%;
		height: 100%;
	}

	.hotspot-text {
        width: 100%; /* 确保宽度占满容器 */
        text-align: left; /* 文字居中 */
        font-size: 30rpx; /* 设置字体大小 */
		font-weight: bold;
        color: #333; /* 设置字体颜色 */
        margin: 50rpx 0; /* 上下边距，根据需要调整 */
		margin-left: 50rpx;
    }

    .hotspot-items {
		column-count: 2; /* 设置两列 */
		column-gap: 16px; /* 列间距 */
		width: 100%; /* 占满宽度 */
	}

	.hotspot-item {
		margin-bottom: 16px; /* 每个item之间的间距 */
		border: 1px solid #e0e0e0;
		border-radius: 10px;
		overflow: hidden;
		box-sizing: border-box; /* 边框和内边距包含在宽度内 */
		break-inside: avoid; /* 防止item被拆分到不同列 */
	}


    .item-image {
        width: 100%;
        /*height: auto;*/ /* 根据图片比例自动调整高度 */
    }

    .item-info {
        padding: 20rpx;
    }

    .item-title {
        font-size: 34rpx;
        color: #333;
        font-weight: bold;
    }

    .item-description {
        font-size: 28rpx;
        color: #666;
        margin-top: 10rpx;
    }

	.icon-text {
		margin-top: 10rpx;
		text-align: center;
		font-size: 24rpx;
		color: #333;
	}

	.navbar {
        display: flex;
        justify-content: space-around;
        position: fixed;
        bottom: 0;
        left: 0;
        width: 100%;
        height: 80px; /* 可以根据需要调整高度 */
        background-color: #fff;
        box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.1);
    }

    .nav-item {
        flex-grow: 1;
        text-align: center;
        align-items: center;
        display: flex;
        flex-direction: column;
        justify-content: center;
    }

    .nav-icon {
        width: 24px; /* 根据需要调整 */
        height: 24px; /* 根据需要调整 */
    }

    .nav-text {
        font-size: 14px; /* 根据需要调整 */
        color: #666; /* 根据需要调整 */
    }


</style>

