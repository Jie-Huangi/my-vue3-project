<template>
  <view class="memo-container">
    <view class="memo-header">
      <text class="memo-title">备忘录</text>
    </view>
    
    <view class="memo-grid">
      <view class="memo-item" v-for="(item, index) in memoList" :key="index" @tap="viewMemo(item)">
        <view class="memo-item-title">{{item.title}}</view>
        <view class="memo-item-content">{{item.content}}</view>
      </view>
      
      <view class="memo-add-btn" @tap="addNewMemo">
        <text class="add-icon">+</text>
      </view>
    </view>
  </view>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { onShow } from '@dcloudio/uni-app'

const memoList = ref([])

function loadMemoList() {
  const data = uni.getStorageSync('memoList')
  if (data && Array.isArray(data)) {
    memoList.value = data
  } else {
    memoList.value = []
  }
}

function viewMemo(item) {
  uni.navigateTo({
    url: `/pages/memo/detail?id=${item.id}`
  })
}

function addNewMemo() {
  uni.navigateTo({
    url: '/pages/memo/add'
  })
}

onMounted(loadMemoList)
onShow(loadMemoList)
</script>

<style lang="scss">
page {
  background-color: #b3b7ee;
  width: 100%;
  height: 100%;
}

.memo-container {
  width: 100%;
  min-height: 100vh;
  padding: 30rpx;
  box-sizing: border-box;
}

.memo-header {
  padding: 20rpx 0 40rpx;
}

.memo-title {
  font-size: 48rpx;
  font-weight: bold;
  color: #FFFFFF;
}

.memo-grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.memo-item {
  width: 48%;
  background-color: #FFFFFF;
  border-radius: 16rpx;
  padding: 24rpx;
  margin-bottom: 30rpx;
  box-sizing: border-box;
  box-shadow: 0 4rpx 12rpx rgba(0, 0, 0, 0.05);
  min-height: 200rpx;
  display: flex;
  flex-direction: column;
}

.memo-item-title {
  font-size: 30rpx;
  font-weight: bold;
  color: #333;
  margin-bottom: 16rpx;
}

.memo-item-content {
  font-size: 26rpx;
  color: #666;
  line-height: 1.5;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 5;
  -webkit-box-orient: vertical;
}

.memo-add-btn {
  width: 48%;
  background-color: #FFFFFF;
  border-radius: 16rpx;
  margin-bottom: 30rpx;
  box-sizing: border-box;
  box-shadow: 0 4rpx 12rpx rgba(0, 0, 0, 0.05);
  min-height: 200rpx;
  display: flex;
  align-items: center;
  justify-content: center;
}

.add-icon {
  font-size: 80rpx;
  color: #b3b7ee;
  font-weight: 300;
}
</style> 