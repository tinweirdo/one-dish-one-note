<template>
    <view class="menu-section">
        <view class="category-list" v-if="!showDishForm">
            <view v-for="(cat, idx) in categories" :key="cat.id"
                :class="['category-item', idx === currentIndex ? 'active' : '']" @click="selectCategory(idx)">
                <text class="cat-icon">{{ cat.icon }}</text>
                <text class="cat-name">{{ cat.name }}</text>
            </view>
        </view>

        <view class="dish-list" v-if="!showDishForm && categories.length > 0">
            <view class="dish-category-title">
                <text>{{ categories[currentIndex].name }}</text>
                <text class="cat-icon">{{ categories[currentIndex].icon }}</text>
            </view>
            <view v-for="dish in categories[currentIndex].dishes" :key="dish.id" class="dish-item"
                @click="editDish(dish.id)">
                <image class="dish-icon" :src="dish.icon" />
                <view class="dish-info">
                    <view class="dish-title-row">
                        <text class="dish-name">{{ dish.name }}</text>
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

            <view class="dish-list-bottom" @click="addDish">
                <span class="add-icon">+</span>
                <span class="add-text">添加商品</span>
            </view>
        </view>
        <dish v-if="showDishForm" :category-id="currentCategoryId" :id="currentDishId" @close="onDishFormClose"
            @saved="onDishFormSaved" />
    </view>
</template>
<script>
import Dish from './dish.vue'

export default {
    components: { Dish },
    data() {
        return {
            currentIndex: 0,
            categories: [],
            showDishForm: false,
            currentCategoryId: null,
            currentDishId: null
        }
    },
    beforeMount() {
        this.fetchAllCategory();
    },
    methods: {
        selectCategory(idx) {
            this.currentIndex = idx
        },
        fetchAllCategory() {
            // 先请求所有分类
            wx.request({
                url: `http://localhost:3000/category`,
                method: 'GET',
                success: (catRes) => {
                    // 再请求所有菜品
                    wx.request({
                        url: `http://localhost:3000/dish`,
                        method: 'GET',
                        success: (dishRes) => {
                            // 假设每个菜品有 categoryId 字段
                            const dishes = dishRes.data;
                            this.categories = catRes.data.map(category => ({
                                ...category,
                                dishes: dishes.filter(dish => dish.pid === category.id)
                            }));
                        },
                        fail: (err) => {
                            console.error('获取菜品失败', err);
                        }
                    });
                },
                fail: (err) => {
                    console.error('获取分类失败', err);
                }
            });
        },
        editDish(id) {
            this.currentDishId = id;
            this.showDishForm = true;
        },
        addDish() {
            this.currentDishId = null;
            const currentCategory = this.categories[this.currentIndex];
            this.currentCategoryId = currentCategory.id;
            this.showDishForm = true;
        },
        onDishFormClose() {
            this.showDishForm = false;
        },
        onDishFormSaved(data) {
            wx.request({
                url: http://localhost:3000/dish,
                method: 'POST',
                data,
                success: (dishRes) => {
                    console.log('dishRes :>> ', dishRes);
                },
                fail: (err) => {
                    console.error('获取菜品失败', err);
                }
            });
            this.showDishForm = false;
            // 可选：刷新菜品列表
            this.fetchAllCategory();
        }
    }
}
</script>
<style scoped>
.menu-section {
    position: relative;
    top: 190rpx;
    display: flex;
    flex-direction: row;
    background: #fff;
    height: calc(100vh - 190rpx);
    overflow: scroll;
}

.category-list {
    height: 100%;
    width: 230rpx;
    overflow-y: scroll;
    background: #f8f8f8;
    display: flex;
    flex-direction: column;
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

.cat- {
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
    display: flex;
    align-items: center;
    margin-bottom: 20rpx;
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

.dish-icon {
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

.dish-list-bottom {
    font-size: 25rpx;
    border-radius: 15rpx;
    padding: 20rpx;
    background-color: #f6f6f6;
    color: #949494;
    text-align: center;
}

.dish-list-bottom>.add-icon {
    margin-right: 15rpx;
}
</style>