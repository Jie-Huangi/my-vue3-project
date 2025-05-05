<template>
  <view class="home-container">
    <view class="header">
      <text class="app-title">备忘录应用</text>
      <view class="user-actions">
        <view class="action-btn" @tap="goToLogin">
          <text class="action-icon">👤</text>
          <text class="action-text">登录/注册</text>
        </view>
      </view>
    </view>
    
    <view class="welcome-section">
      <image class="logo" src="/static/logo.png"></image>
      <text class="welcome-title">欢迎使用备忘录应用</text>
      <text class="welcome-subtitle">随时记录您的想法和待办事项</text>
    </view>
    
    <view class="feature-section">
      <view class="feature-title">功能介绍</view>
      
      <view class="feature-grid">
        <view class="feature-item" @tap="goToMemo">
          <text class="feature-icon">📝</text>
          <text class="feature-name">备忘录</text>
          <text class="feature-desc">记录您的想法和灵感</text>
        </view>
        
        <view class="feature-item coming-soon">
          <text class="feature-icon">📅</text>
          <text class="feature-name">日历</text>
          <text class="feature-desc">即将推出</text>
        </view>
        
        <view class="feature-item coming-soon">
          <text class="feature-icon">⏰</text>
          <text class="feature-name">提醒</text>
          <text class="feature-desc">即将推出</text>
        </view>
        
        <view class="feature-item coming-soon">
          <text class="feature-icon">🔍</text>
          <text class="feature-name">搜索</text>
          <text class="feature-desc">即将推出</text>
        </view>
      </view>
    </view>
    
    <view class="footer">
      <text class="footer-text">© 2025 备忘录应用</text>
    </view>
  </view>
</template>

<script setup>
import { ref } from 'vue'

// 检查是否已登录
const isLoggedIn = ref(false)

// 导航方法
function goToLogin() {
  uni.navigateTo({
    url: '/pages/login/index'
  })
}

function goToMemo() {
  uni.switchTab({
    url: '/pages/memo/index'
  })
}
</script>

<style lang="scss">
page {
  background-color: #f8f9fc;
  width: 100%;
  height: 100%;
}

.home-container {
  width: 100%;
  min-height: 100vh;
  padding-bottom: 100rpx;
  box-sizing: border-box;
}

.header {
  background-color: #b3b7ee;
  padding: 80rpx 30rpx 30rpx;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.app-title {
  font-size: 36rpx;
  font-weight: bold;
  color: #FFFFFF;
}

.user-actions {
  display: flex;
}

.action-btn {
  display: flex;
  align-items: center;
  background-color: rgba(255, 255, 255, 0.2);
  padding: 10rpx 20rpx;
  border-radius: 30rpx;
}

.action-icon {
  font-size: 32rpx;
  margin-right: 10rpx;
}

.action-text {
  font-size: 24rpx;
  color: #FFFFFF;
}

.welcome-section {
  padding: 60rpx 30rpx;
  text-align: center;
}

.logo {
  height: 160rpx;
  width: 160rpx;
  margin-bottom: 30rpx;
}

.welcome-title {
  font-size: 40rpx;
  font-weight: bold;
  color: #333;
  margin-bottom: 20rpx;
}

.welcome-subtitle {
  font-size: 28rpx;
  color: #666;
}

.feature-section {
  padding: 30rpx;
}

.feature-title {
  font-size: 32rpx;
  font-weight: bold;
  color: #333;
  margin-bottom: 30rpx;
}

.feature-grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.feature-item {
  width: 48%;
  background-color: #FFFFFF;
  border-radius: 16rpx;
  padding: 30rpx;
  margin-bottom: 30rpx;
  box-sizing: border-box;
  box-shadow: 0 4rpx 12rpx rgba(0, 0, 0, 0.05);
  display: flex;
  flex-direction: column;
  align-items: center;
}

.feature-icon {
  font-size: 60rpx;
  margin-bottom: 20rpx;
}

.feature-name {
  font-size: 28rpx;
  font-weight: bold;
  color: #333;
  margin-bottom: 10rpx;
}

.feature-desc {
  font-size: 24rpx;
  color: #999;
  text-align: center;
}

.coming-soon {
  opacity: 0.6;
}

.footer {
  text-align: center;
  padding: 40rpx 0;
}

.footer-text {
  font-size: 24rpx;
  color: #999;
}
</style>
