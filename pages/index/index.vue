<template>
  <view class="container">
    <!-- 顶部搜索栏 -->
    <u-search placeholder="菜谱名称/食材" v-model="search" :show-action="true" action-text="搜索" @search="onSearch" bg-color="#fff0f6" color="#ff5a5f" border-radius="24" />

    <!-- 菜谱列表 -->
    <scroll-view scroll-y class="category-list">
      <view v-for="(category, idx) in categories" :key="idx" class="category">
        <view class="category-title">{{ category.name }}</view>
        <u-card v-for="(dish, didx) in category.dishes" :key="didx" :title="dish.name" :sub-title="'已售' + dish.sold" :thumb="dish.img" :border="false" :body-style="{padding: '10rpx 0'}" :head-style="{background:'#fff'}" :foot-style="{background:'#fff'}" class="dish-card">
          <view class="dish-info">
            <text class="dish-price">￥{{ dish.price }}</text>
            <u-button type="primary" shape="circle" size="mini" color="#ff5a5f" @click="addToCart(dish)">+</u-button>
          </view>
        </u-card>
      </view>
    </scroll-view>

    <!-- 购物车区 -->
    <view class="cart-bar">
      <u-icon name="shopping-cart" color="#ff5a5f" size="48"></u-icon>
      <view class="cart-info">
        <text>购物车</text>
        <text class="cart-count">{{ cart.length }}</text>
      </view>
      <u-button class="cart-btn" type="default" color="#fff0f6" text-color="#ff5a5f" shape="circle" size="medium">邀请下单</u-button>
      <u-button class="cart-btn" type="primary" color="#ff5a5f" shape="circle" size="medium">下单</u-button>
    </view>

    <!-- 底部导航栏 -->
    <u-tabbar :value="tabIndex" @change="onTabChange" active-color="#ff5a5f" inactive-color="#888" :fixed="true" :safe-area-inset-bottom="true">
      <u-tabbar-item icon="home">共享厨房</u-tabbar-item>
      <u-tabbar-item icon="share">分享</u-tabbar-item>
      <u-tabbar-item icon="account">个人中心</u-tabbar-item>
    </u-tabbar>
  </view>
</template>

<script>
export default {
  data() {
    return {
      search: '',
      tabIndex: 0,
      cart: [],
      categories: [
        {
          name: '健康蔬菜',
          dishes: [
            { name: '清炒油麦菜', img: '/static/logo.png', price: 5, sold: 0 },
            { name: '清炒莴苣片', img: '/static/logo.png', price: 8, sold: 0 }
          ]
        },
        {
          name: '大肉肉',
          dishes: [
            { name: '炒生菜', img: '/static/logo.png', price: 5, sold: 0 }
          ]
        }
        // 你可以继续添加其他分类和菜品
      ]
    }
  },
  methods: {
    onSearch(val) {
      // 搜索逻辑，可根据val过滤categories
      // 这里只做简单提示
      uni.showToast({ title: '搜索：' + val, icon: 'none' })
    },
    addToCart(dish) {
      this.cart.push(dish)
    },
    onTabChange(index) {
      this.tabIndex = index
      // 可根据index跳转页面
    }
  }
}
</script>

<style>
.container {
  background: #fff;
  min-height: 100vh;
  padding-bottom: 220rpx;
}
.category-list {
  margin-bottom: 20rpx;
  max-height: 60vh;
}
.category-title {
  font-size: 28rpx;
  font-weight: bold;
  margin: 20rpx 0 10rpx 10rpx;
  color: #ff5a5f;
}
.dish-card {
  margin-bottom: 18rpx;
  border-radius: 16rpx;
  box-shadow: 0 2rpx 12rpx #ffe4ec;
}
.dish-info {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 10rpx;
}
.dish-price {
  color: #ff5a5f;
  font-size: 28rpx;
  font-weight: bold;
}
.cart-bar {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 120rpx;
  z-index: 10;
  background: #fff0f6;
  display: flex;
  align-items: center;
  padding: 18rpx 30rpx;
  box-shadow: 0 -2rpx 10rpx #ffe4ec;
  border-radius: 32rpx 32rpx 0 0;
}
.cart-info {
  flex: 1;
  margin-left: 18rpx;
  color: #ff5a5f;
  font-size: 26rpx;
}
.cart-count {
  margin-left: 8rpx;
  background: #ff5a5f;
  color: #fff;
  border-radius: 50%;
  padding: 2rpx 10rpx;
  font-size: 22rpx;
}
.cart-btn {
  margin-left: 18rpx;
}
</style>
