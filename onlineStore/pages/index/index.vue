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

		<view class="button-group">
			<view
				class="filter-button"
				v-for="(button, index) in buttons"
				:key="index"
				:class="{ active: activeButton === index }"
				@click="onButtonClick(index)"
			>
				{{ button.label }}
			</view>
			</view>

			<view class="hotspot-items">
			<view
				class="hotspot-item"
				v-for="(item, index) in filteredItems"
				:key="index"
			>
				<image :src="item.imgSrc" mode="widthFix" class="item-image"></image>
				<view class="item-info">
				<text class="item-title">{{ item.title }}</text>
				<text class="item-description">{{ item.description }}</text>
				</view>
			</view>
		</view>

		<view class="navbar">
			<view
				class="nav-item"
				v-for="(item, index) in navbarItems"
				:key="index"
				:class="{ active: index === 0 }"
				@click="onNavClick(index)"
			>
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
				buttons: [
					{ label: '近期热点', category: 'hot' },
					{ label: '推荐商品', category: 'recommend' },
					{ label: '新品上市', category: 'new' },
				],
				activeButton: 0, // 默认高亮第一个按钮
				hotspotItems: [
					{ imgSrc: "/static/img/product1.jpg", title: "商品标题1", description: "描述信息1", category: "hot" },
					{ imgSrc: "/static/img/product2.jpg", title: "商品标题2", description: "描述信息2", category: "hot" },
					{ imgSrc: "/static/img/product3.jpg", title: "商品标题3", description: "描述信息3", category: "recommend" },
					{ imgSrc: "/static/img/product4.jpg", title: "商品标题4", description: "描述信息4", category: "new" },
					// 更多商品
				],
				activeNavbar: 0, // 默认第一个选中
				navbarItems: [
					{ icon: 'fa fa-home', text: '首页' },
					{ icon: 'fa fa-th', text: '分类' },
					{ icon: 'fa fa-shopping-cart', text: '购物车' },
					{ icon: 'fa fa-user', text: '我的' },
				],
			}
		},
		onLoad() {

		},

		computed: {
			filteredItems() {
			// 根据选中的按钮类别筛选瀑布流内容
			const activeCategory = this.buttons[this.activeButton].category;
			return this.hotspotItems.filter(item => item.category === activeCategory);
			},
		},

		methods: {
			onButtonClick(index) {
				this.activeButton = index; // 设置当前高亮按钮
			},
			onNavClick(index) {
				if (index === 0) {
					// 跳转到首页
					uni.switchTab({
						url: '/pages/index/index'
					});
				} else if (index === 1) {
					// 跳转到分类页面
					uni.navigateTo({
						url: '/pages/index/category'
					});
				} else if (index === 2) {
					// 跳转到购物车页面
					uni.navigateTo({
						url: '/pages/index/shoppingCart'
					});
				} else if (index === 3) {
					// 跳转到我的页面
					uni.navigateTo({
						url: '/pages/index/myProfile'
					});
				}
			},
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: flex-start;
		justify-content: center;
		width: 100%;
		overflow: hidden;
		background: linear-gradient(to bottom, #ADD8E6, #ffffff); /* 从蓝色到白色 */
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
		display: block; /* 让整个框单独占一行 */
		width: auto; /* 根据内容自适应宽度 */
		text-align: left; /* 确保文字内容左对齐 */
		font-size: 35rpx; /* 字体大小 */
		font-weight: bold; /* 字体加粗 */
		color: #333; /* 设置文字颜色 */
		margin: 50rpx 0; /* 上下边距 */
		margin-left: 20rpx; /* 左边距，让框靠左 */
		background-color: #fff; /* 背景颜色 */
		border-radius: 20rpx; /* 圆角边框 */
		padding: 10rpx 40rpx; /* 内边距 */
		box-shadow: 0 4rpx 8rpx rgba(0, 0, 0, 0.1); /* 添加阴影 */
	}

	.button-group {
		display: flex;
		justify-content: space-around; /* 按钮靠左对齐 */
		margin: 20rpx; /* 外边距 */
		gap: 10rpx; /* 按钮间距 */
		width:100%;
	}

	.filter-button {
		padding: 10rpx 20rpx;
		background-color: #fff; /* 默认背景色 */
		color: #333;
		border: 1rpx solid #ccc;
		border-radius: 20rpx;
		font-size: 28rpx;
		cursor: pointer;
		transition: all 0.3s ease; /* 添加过渡动画 */
	}

	.filter-button.active {
		background-color: #77cfed; /* 高亮时背景色变浅蓝 */
		color: #fff; /* 高亮时文字变白 */
		border-color: #87CEEB; /* 边框变浅蓝 */
	}

    .hotspot-items {
		column-count: 2; /* 设置两列 */
		column-gap: 16px; /* 列间距 */
		width: 100%; /* 占满宽度 */
		padding-bottom: 80px; /* 预留出 navbar 的高度，80px 是你的 navbar 高度 */
	}

	.hotspot-item {
		margin-bottom: 16px; /* 每个item之间的间距 */
		border: 1px solid #e0e0e0;
		border-radius: 10px;
		overflow: hidden;
		box-sizing: border-box; /* 边框和内边距包含在宽度内 */
		break-inside: avoid; /* 防止item被拆分到不同列 */
		background-color: #fff;
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
		height: 80px; /* 导航栏高度 */
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
		color: #666; /* 默认文字颜色 */
	}

	.nav-item.active {
		color: #1E90FF; /* 高亮文字和图标颜色（蓝色） */
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

