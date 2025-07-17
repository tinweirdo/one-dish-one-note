<template>
    <view class="dish-form">
        <view class="form-item">
            <text class="label">菜名：</text>
            <input v-model="dish.name" placeholder="请输入菜品名称" />
        </view>
        <view class="form-item">
            <text class="label">图片：</text>
            <button @click="chooseImage" class="image-btn">选择图片</button>
            <image v-if="dish.icon" :src="dish.icon" class="dish-image-preview" />
        </view>
        <view class="form-item">
            <text class="label">价格：</text>
            <input v-model="dish.price" type="number" placeholder="请输入价格" />
        </view>
        <view class="form-item">
            <text class="label">评分：</text>
            <input v-model="dish.score" type="number" placeholder="请输入评分" />
        </view>
        <view class="form-item">
            <text class="label">备注：</text>
            <input v-model="dish.remark" placeholder="请输入备注" />
        </view>
        <view class="form-actions">
            <button class="back-btn" @click="onBack">返回</button>
            <button class="submit-btn" @click="submitDish">保存</button>
        </view>
    </view>
</template>
<script>
export default {
    props: {
        categoryId: {
            type: [String, Number],
            required: true
        }
    },
    data() {
        return {
            dish: {
                name: '',
                icon: '',
                price: '',
                score: '',
                remark: ''
            }
        }
    },
    methods: {
        chooseImage() {
            // 选择图片，兼容微信小程序/uniapp
            uni.chooseImage({
                count: 1,
                success: (res) => {
                    this.dish.icon = res.tempFilePaths[0];
                }
            });
        },
        submitDish() {
            // 这里可以做表单校验和提交逻辑
            console.log('提交菜品信息：', { ...this.dish, pid: this.categoryId });
            // TODO: 实际保存逻辑
            this.$emit('saved');
        },
        onBack() {
            this.$emit('close');
        }
    }
}
</script>
<style>
.dish-form {
    padding: 30rpx;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}
.form-item {
    display: flex;
    align-items: center;
    margin-bottom: 30rpx;
}
.label {
    width: 120rpx;
    font-size: 28rpx;
    color: #333;
}
input {
    flex: 1;
    border: 1rpx solid #eee;
    border-radius: 8rpx;
    padding: 12rpx 20rpx;
    font-size: 28rpx;
    background: #fafafa;
}
.dish-image-preview {
    width: 100rpx;
    height: 100rpx;
    margin-left: 20rpx;
    border-radius: 8rpx;
    border: 1rpx solid #eee;
}
.form-actions {
    display: flex;
    justify-content: space-between;
    width: calc(100% - 60rpx);
}
.back-btn {
    background: #f8f8f8;
    color: #848484;
    font-size: 32rpx;
    border-radius: 12rpx;
    padding: 10rpx 0;
    flex: 1;
    margin-right: 20rpx;
}
.submit-btn {
    background: #fe4a63;
    color: #fff;
    font-size: 32rpx;
    border-radius: 12rpx;
    padding: 10rpx 0;
    flex: 1;
}

.image-btn{
    margin-left: 0;
    height: 50rpx;
    line-height: 50rpx;
    font-size: 28rpx;
}
</style>