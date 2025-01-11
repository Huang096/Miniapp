<!--
 Copyright 2025 huangzheheng
 
 Licensed under the Apache License, Version 2.0 (the "License");
 you may not use this file except in compliance with the License.
 You may obtain a copy of the License at
 
     https://www.apache.org/licenses/LICENSE-2.0
 
 Unless required by applicable law or agreed to in writing, software
 distributed under the License is distributed on an "AS IS" BASIS,
 WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 See the License for the specific language governing permissions and
 limitations under the License.
-->

<template>
  <view class="category-page">
    <scroll-view class="top-icons" scroll-x>
      <!-- 添加一个容器来实现横向排列 -->
      <view class="top-icons-container">
        <view
          class="icon-container"
          v-for="(icon, index) in topIcons"
          :key="index"
          :class="{ active: activeTopIcon === index }"
          @click="onTopIconClick(index)"
        >
          <view class="icon-image">
            <image :src="icon.imgSrc" mode="aspectFill"></image>
          </view>
          <text class="icon-text">{{ icon.text }}</text>
        </view>
      </view>
    </scroll-view>

    <!-- 主内容部分 -->
    <view class="main-content">
      <!-- 左侧侧边栏 -->
      <scroll-view class="side-column-menu" scroll-y>
        <view
          v-for="(menu, index) in sideMenu"
          :key="index"
          class="menu-item"
          :class="{ active: activeSideMenu === index }"
          @click="onSideMenuClick(index)"
        >
          {{ menu.text }}
        </view>
      </scroll-view>

      <!-- 右侧商品内容 -->
      <scroll-view class="product-list" scroll-y>
        <view
          v-for="(product, index) in filteredProducts"
          :key="index"
          class="product-item"
        >
          <image :src="product.imgSrc" class="product-image" />
          <view class="product-info">
            <text class="product-title">{{ product.title }}</text>
            <text class="product-price">¥{{ product.price }}</text>
            <button class="add-to-cart" @click="onAddToCart(product)">
              加入购物车
            </button>
          </view>
        </view>
      </scroll-view>
    </view>

    <!-- 底部购物车和价格 -->
    <view class="cart-summary">
      <view class="cart-icon">
        <image src="/static/icons/cart.png" class="icon" />
        <text>¥{{ totalPrice }}</text>
      </view>
      <button class="checkout-button" @click="goToCheckout">
        去下单
      </button>
    </view>

    <view class="navbar">
			<view
				class="nav-item"
				v-for="(item, index) in navbarItems"
				:key="index"
				:class="{ active: index === 1 }"
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
        topIcons: [
          { imgSrc: "/static/img/icon1.jpg", text: "水果鲜花" },
          { imgSrc: "/static/img/icon1.jpg", text: "蔬菜豆腐" },
          { imgSrc: "/static/img/icon1.jpg", text: "肉禽蛋品" },
          { imgSrc: "/static/img/icon1.jpg", text: "海鲜水产" },
        ],
        activeTopIcon: 0, // 默认选中第一个

        sideMenu: [
          { text: "category1" },
          { text: "category2" },
          { text: "category3" },
          { text: "category4" },
        ],
        activeSideMenu: 0, // 默认选中第一个

        products: [
          { imgSrc: "/static/products/product1.jpg", title: "商品1", price: 10, category: 0 },
          { imgSrc: "/static/products/product2.jpg", title: "商品2", price: 20, category: 1 },
          { imgSrc: "/static/products/product3.jpg", title: "商品3", price: 30, category: 0 },
          { imgSrc: "/static/products/product4.jpg", title: "商品4", price: 40, category: 2 },
        ],
        cart: [],
        totalPrice: 0,

        activeNavbar: 1, // 这页是第二个被选中
        navbarItems: [
            { icon: 'fa fa-home', text: '首页' },
            { icon: 'fa fa-th', text: '分类' },
            { icon: 'fa fa-shopping-cart', text: '购物车' },
            { icon: 'fa fa-user', text: '我的' }
          ],
      };
    },
    computed: {
      filteredProducts() {
        return this.products.filter(
          (product) => product.category === this.activeSideMenu
        );
      },
    },
    methods: {
      onTopIconClick(index) {
        this.activeTopIcon = index;
      },
      onSideMenuClick(index) {
        this.activeSideMenu = index;
      },
      onAddToCart(product) {
        this.cart.push(product);
        this.totalPrice += product.price;
      },
      goToCheckout() {
        uni.navigateTo({ url: "/pages/cart/cart" });
      },
      onNavClick(index) {
				if (index === 0) {
					// 跳转到首页
					uni.navigateTo({
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
    },
  };
</script>

<style>
  .category-page {
    display: flex;
    flex-direction: column;
    height: 100vh;
  }

  .top-icons-container {
    display: flex;
    flex-direction: row;
  }


  .top-icons {
    display: flex;
    flex-direction: row; /* 横向排列 */
    overflow-x: scroll;  /* 启用水平滚动 */
    white-space: nowrap; /* 防止子元素换行 */
    background-color: #fff;
    padding: 10rpx 0;
    border-bottom: 1px solid #eee;
  }

  .icon-container {
    display: flex;
    flex-direction: column; /* 垂直排列 */
    align-items: center;    /* 水平居中对齐 */
    width: 80rpx;          /* 图标容器的宽度 */
    margin: 0 10rpx;        /* 图标间的水平间距 */
  }

  .icon-image {
    width: 60rpx;           /* 图标宽度 */
    height: 60rpx;          /* 图标高度 */
    border-radius: 50%;     /* 圆形图标 */
    overflow: hidden;       /* 超出部分隐藏 */
    background-color: #f8f8f8; /* 可选：设置背景颜色 */
    margin-bottom: 5rpx;    /* 图片与文字间距 */
  }

  .icon-image image {
    width: 100%;
    height: 100%;
  }

  .icon-text {
    font-size: 24rpx;
    color: #333; /* 默认颜色 */
  }

  .icon-container.active .icon-text {
    color: #1e90ff; /* 选中状态颜色 */
  }

  .main-content {
    display: flex;
    flex: 1;
  }

  .side-column-menu {
    width: 100px;
    background-color: #f8f8f8;
    overflow-y: scroll;
  }

  .menu-item {
    padding: 10px;
    text-align: center;
  }

  .menu-item.active {
    background-color: #1e90ff;
    color: #fff;
  }

  .product-list {
    flex: 1;
    background-color: #fff;
    overflow-y: scroll;
    padding: 10px;
  }

  .product-item {
    display: flex;
    border-bottom: 1px solid #eee;
    padding: 10px 0;
  }

  .product-image {
    width: 80px;
    height: 80px;
  }

  .product-info {
    flex: 1;
    padding-left: 10px;
  }

  .add-to-cart {
    background-color: #1e90ff;
    color: white;
    border: none;
    padding: 5px 10px;
    border-radius: 5px;
  }

  .cart-summary {
    position: fixed;
    bottom: 80px; /* 导航栏高度 */
    left: 0;
    right: 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 5px;
    background-color: #fff;
    border-top: 1px solid #eee;
    z-index: 100; /* 确保它位于导航栏之上 */
    width: 100%;
    overflow: visible; /* 确保子元素不会被裁剪 */
    padding: 10px 0px; /* 增加左右内边距 */
  }


  .cart-icon {
    display: flex;
    align-items: center;
  }

  .cart-icon .icon {
    width: 24px;
    height: 24px;
  }

  .checkout-button {
    flex-shrink: 0;
    /* 保留原有样式 */
    background-color: #ff4500;
    color: #fff;
    padding: 5px 8px;
    border-radius: 5px;
    font-size: 14px;
    margin: 0;
    width: auto;
    box-sizing: border-box;
    position: relative;
    margin: 0 30px 0 0; /* 这里设置右边距为10px，或根据需要调整 */
  }


  .checkout-button::after {
    content: none; /* 确保没有伪元素占用空间 */
  }


  .bottom-menu {
    display: flex;
    justify-content: space-around;
    background-color: #fff;
    border-top: 1px solid #eee;
  }

  .menu-item {
    text-align: center;
    padding: 10px 0;
  }

  .menu-icon {
    width: 24px;
    height: 24px;
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