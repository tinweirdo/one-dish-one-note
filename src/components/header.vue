<template>
    <view class="user-header">
        <view class="user-left">
            <image class="avatar"
                src="https://cdn.jsdelivr.net/gh/tinweirdo/images/2025/d78575cf108e4547cf369ff8999dfff1.jpg" />
            <view class="user-info">
                <view class="user-name-row">
                    <text class="user-name">婷</text>
                    <text class="user-role boss">老板</text>
                </view>
            </view>
        </view>
        <view class="header-center">
            <view class="user-level">
                <text class="level-label">LV</text>
                <text class="level-num">1</text>
            </view>
        </view>
        <view class="user-right">
            <image class="avatar"
                src="https://cdn.jsdelivr.net/gh/tinweirdo/images/2025/d8ae9e5ce0fbd21612a0c9b5bd6d64c8.jpg" />
            <view class="user-info">
                <view class="user-name-row">
                    <text class="user-name">官</text>
                    <text class="user-role customer">顾客</text>
                </view>
            </view>
        </view>
    </view>
</template>
<script>
export default {
}
</script>
<style scoped>
.user-header {
    position: fixed;
    top: 0;
    width: calc(100% - 80rpx);
    height: 60px;
    background: #fe4a63;
    padding: 20rpx 40rpx;
    display: flex;
    align-items: center;
    justify-content: space-between;
    color: #fff;
}

.user-left,
.user-right {
    display: flex;
    align-items: center;
}

.avatar {
    width: 90rpx;
    height: 90rpx;
    border-radius: 50%;
    border: 4rpx solid #fff;
}

.user-info {
    margin-left: 16rpx;
}

.user-name-row {
    display: flex;
    align-items: center;
}

.user-name {
    font-size: 30rpx;
    font-weight: bold;
}

.user-role {
    font-size: 22rpx;
    margin-left: 10rpx;
    padding: 2rpx 16rpx;
    border-radius: 20rpx;
    background: #fff;
    color: #fe4a63;
}

.user-role.boss {
    background: #fff;
    color: #fe4a63;
}

.user-role.customer {
    background: #fff;
    color: #fe4a63;
}

.user-level {
    display: flex;
    align-items: center;
}

.level-label {
    width: 25rpx;
    height: 25rpx;
    background: #fff;
    border: 2rpx solid #fe4a63;
    color: #fe4a63;
    border-radius: 50%;
    font-weight: bold;
    font-size: 16rpx;
    line-height: 30rpx;
    z-index: 2;
    padding: 5rpx;
}

.level-num {
    width: 40rpx;
    height: 25rpx;
    line-height: 30rpx;
    background: #fff;
    color: #fe4a63;
    font-size: 16rpx;
    font-weight: bold;
    margin-left: -10rpx;
    /* 让左圆和右方形无缝拼接并有轻微重叠 */
    padding-left: 7rpx;
    z-index: 1;
    box-shadow: 0 0 2rpx #eee;
}

.header-center {
    flex: 1;
    text-align: center;
    font-size: 32rpx;
    font-weight: bold;
    display: flex;
    align-items: center;
    justify-content: center;
}
</style>