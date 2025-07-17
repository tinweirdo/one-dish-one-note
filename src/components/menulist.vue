<template>
    <view class="menu-section">
        <view class="category-list">
            <view v-for="(cat, idx) in categories" :key="cat.id"
                :class="['category-item', idx === currentCategory ? 'active' : '']" @click="selectCategory(idx)">
                <text class="cat-emoji">{{ cat.emoji }}</text>
                <text class="cat-name">{{ cat.name  }}</text>
            </view>
        </view>
        <view class="dish-list">
            <view class="dish-category-title">
                <text>{{ categories[currentCategory].name }}</text>
                <text class="cat-emoji">{{ categories[currentCategory].emoji }}</text>
            </view>
            <view v-for="dish in categories[currentCategory].dishes" :key="dish.id" class="dish-item">
                <image class="dish-img" :src="dish.img" />
                <view class="dish-info">
                    <view class="dish-title-row">
                        <text class="dish-name">{{ dish.name  }}</text>
                        <view class="dish-like">
                            <u-icon name="heart-fill" color="#fe4a63" size="22" />
                            <text class="like-num">{{ dish.likes }}</text>
                        </view>
                    </view>
                    <text class="dish-sold">已售{{ dish.sold }}</text>
                </view>
                <view class="dish-actions">
                    <u-icon name="arrow-up" size="22" color="#fe4a63" />
                    <u-icon name="arrow-down" size="22" color="#fe4a63" style="margin-top: 10rpx;" />
                </view>
            </view>
        </view>
    </view>
</template>
<script>
export default {
    data() {
        return {
            currentCategory: 0,
            categories: [
                {
                    id: 1,
                    name: '健康蔬菜',
                    emoji: '🥬',
                    dishes: [
                        { id: 1, name: '清炒藕片', img: '/static/logo.png', sold: 0, likes: 8 },
                        { id: 2, name: '炒生菜', img: '/static/logo.png', sold: 0, likes: 5 },
                        { id: 3, name: '香葱煎蛋', img: '/static/logo.png', sold: 0, likes: 8 },
                        { id: 4, name: '清炒油麦菜', img: '/static/logo.png', sold: 0, likes: 5 },
                        { id: 5, name: '清炒藕片', img: '/static/logo.png', sold: 0, likes: 8 },
                        { id: 6, name: '炒生菜', img: '/static/logo.png', sold: 0, likes: 5 },
                        { id: 7, name: '香葱煎蛋', img: '/static/logo.png', sold: 0, likes: 8 },
                        { id: 8, name: '清炒油麦菜', img: '/static/logo.png', sold: 0, likes: 5 },
                        { id: 9, name: '清炒藕片', img: '/static/logo.png', sold: 0, likes: 8 },
                        { id: 10, name: '炒生菜', img: '/static/logo.png', sold: 0, likes: 5 },
                        { id: 11, name: '香葱煎蛋', img: '/static/logo.png', sold: 0, likes: 8 },
                        { id: 12, name: '清炒油麦菜', img: '/static/logo.png', sold: 0, likes: 5 },
                        { id: 13, name: '清炒藕片', img: '/static/logo.png', sold: 0, likes: 8 },
                        { id: 14, name: '炒生菜', img: '/static/logo.png', sold: 0, likes: 5 },
                        { id: 15, name: '香葱煎蛋', img: '/static/logo.png', sold: 0, likes: 8 },
                        { id: 16, name: '清炒油麦菜', img: '/static/logo.png', sold: 0, likes: 5 },
                        { id: 17, name: '清炒藕片', img: '/static/logo.png', sold: 0, likes: 8 },
                        { id: 18, name: '炒生菜', img: '/static/logo.png', sold: 0, likes: 5 },
                        { id: 19, name: '香葱煎蛋', img: '/static/logo.png', sold: 0, likes: 8 },
                        { id: 20, name: '清炒油麦菜', img: '/static/logo.png', sold: 0, likes: 5 }
                    ]
                },
                {
                    id: 2,
                    name: '肉肉炒菜',
                    emoji: '🥗',
                    dishes: []
                },
                {
                    id: 3,
                    name: '大肉肉',
                    emoji: '🍗',
                    dishes: []
                },
                {
                    id: 4,
                    name: '美味汤羹',
                    emoji: '🍲',
                    dishes: []
                },
                {
                    id: 5,
                    name: '主食',
                    emoji: '🍚',
                    dishes: []
                },
                {
                    id: 6,
                    name: '小食',
                    emoji: '🍡',
                    dishes: []
                },
                {
                    id: 6,
                    name: '小食',
                    emoji: '🍡',
                    dishes: []
                },
                {
                    id: 7,
                    name: '小食',
                    emoji: '🍡',
                    dishes: []
                },
                {
                    id: 8,
                    name: '小食',
                    emoji: '🍡',
                    dishes: []
                },
                {
                    id: 9,
                    name: '小食',
                    emoji: '🍡',
                    dishes: []
                },
                {
                    id: 10,
                    name: '小食',
                    emoji: '🍡',
                    dishes: []
                },
                {
                    id: 11,
                    name: '小食',
                    emoji: '🍡',
                    dishes: []
                },
                {
                    id: 12,
                    name: '小食',
                    emoji: '🍡',
                    dishes: []
                },
                {
                    id: 13,
                    name: '小食',
                    emoji: '🍡',
                    dishes: []
                },
                {
                    id: 14,
                    name: '小食',
                    emoji: '🍡',
                    dishes: []
                },
                {
                    id: 15,
                    name: '小食',
                    emoji: '🍡',
                    dishes: []
                },
                {
                    id: 16,
                    name: '小食',
                    emoji: '🍡',
                    dishes: []
                },
                {
                    id: 17,
                    name: '小食',
                    emoji: '🍡',
                    dishes: []
                }
            ]
        }
    },
    methods: {
        selectCategory(idx) {
            this.currentCategory = idx
        }
    }
}
</script>
<style scoped>
.menu-section {
    display: flex;
    flex-direction: row;
    background: #fff;
    margin-top: 135rpx;
    height: 100vh;
    overflow: scroll;
}

.category-list {
    height: 100%;
    width: 230rpx;
    overflow-y: scroll;
    background: #f8f8f8;
    border-radius: 0 30rpx 30rpx 0;
    padding: 20rpx 0;
    display: flex;
    flex-direction: column;
    align-items: stretch;
}

.category-item {
    padding: 24rpx 0 24rpx 20rpx;
    display: flex;
    align-items: center;
    font-size: 28rpx;
    color: #333;
    cursor: pointer;
    border-left: 8rpx solid transparent;
    background: #f8f8f8;
    transition: background 0.2s;
}

.category-item.active {
    background: #fff;
    color: #fe4a63;
    border-left: 8rpx solid #fe4a63;
    font-weight: bold;
}

.cat-emoji {
    font-size: 32rpx;
    margin-right: 10rpx;
}

.cat-name {
    font-size: 28rpx;
}

.dish-list {
    height: 100%;
    overflow-y: scroll;
    flex: 1;
    padding: 20rpx 20rpx 0 20rpx;
}

.dish-category-title {
    font-size: 30rpx;
    font-weight: bold;
    color: #222;
    margin-bottom: 18rpx;
    display: flex;
    align-items: center;
}

.dish-item {
    display: flex;
    align-items: center;
    background: #fff;
    border-radius: 18rpx;
    box-shadow: 0 2rpx 12rpx #ffe4ec;
    margin-bottom: 18rpx;
    padding: 16rpx 10rpx;
}

.dish-img {
    width: 110rpx;
    height: 110rpx;
    border-radius: 12rpx;
    margin-right: 18rpx;
}

.dish-info {
    flex: 1;
}

.dish-title-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.dish-name {
    font-size: 28rpx;
    font-weight: bold;
    color: #222;
}

.dish-like {
    display: flex;
    align-items: center;
}

.like-num {
    color: #fe4a63;
    font-size: 24rpx;
    margin-left: 6rpx;
}

.dish-sold {
    color: #888;
    font-size: 22rpx;
    margin-top: 8rpx;
    display: block;
}

.dish-actions {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-left: 10rpx;
}
</style>