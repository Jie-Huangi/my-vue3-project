<template>
  <view class="login-container">
    <view class="login-card">
      <view class="login-header">
        <view class="login-title">欢迎回来</view>
        <view class="login-subtitle">请登录您的账号</view>
      </view>
      
      <view class="login-form">
        <view class="form-item">
          <view class="form-label">用户名</view>
          <view class="input-wrapper">
            <text class="icon">👤</text>
            <input 
              class="form-input" 
              type="text" 
              v-model="username" 
              placeholder="请输入用户名" 
            />
          </view>
        </view>
        
        <view class="form-item">
          <view class="form-label">密码</view>
          <view class="input-wrapper">
            <text class="icon">🔒</text>
            <input 
              class="form-input" 
              :type="showPassword ? 'text' : 'password'" 
              v-model="password" 
              placeholder="请输入密码" 
            />
          </view>
        </view>
        
        <view class="options-row">
          <view class="remember-me" @tap="toggleRememberMe">
            <view class="checkbox" :class="{ active: rememberMe }"></view>
            <text class="remember-text">记住我</text>
          </view>
          <view class="forgot-password" @tap="forgotPassword">忘记密码?</view>
        </view>
        
        <button class="login-button" @tap="handleLogin">登 录</button>
        
        <view class="register-link">
          <text>还没有账号？</text>
          <text class="register-text" @tap="goToRegister">立即注册</text>
        </view>
      </view>
    </view>
  </view>
</template>

<script setup>
import { ref } from 'vue'

// 响应式状态
const username = ref('')
const password = ref('')
const showPassword = ref(false)
const rememberMe = ref(false)

// 方法
const togglePasswordVisibility = () => {
  showPassword.value = !showPassword.value
}

const toggleRememberMe = () => {
  rememberMe.value = !rememberMe.value
}

const handleLogin = () => {
  if (!username.value || !password.value) {
    uni.showToast({
      title: '请输入用户名和密码',
      icon: 'none'
    })
    return
  }
  
  // 模拟登录请求
  uni.showLoading({ title: '登录中...' })
  
  setTimeout(() => {
    uni.hideLoading()
    uni.showToast({
      title: '登录成功',
      icon: 'success'
    })
    
    // 登录成功后跳转到备忘录页面
    setTimeout(() => {
      uni.redirectTo({
        url: '/pages/memo/index'
      })
    }, 1500)
  }, 1500)
}

const forgotPassword = () => {
  uni.showToast({
    title: '忘记密码功能开发中',
    icon: 'none'
  })
}

const goToRegister = () => {
  uni.navigateTo({
    url: '/pages/register/index'
  })
}
</script>

<style lang="scss">
page {
  background-color: #b3b7ee;
  width: 100%;
  height: 100%;
}

.login-container {
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 30rpx;
  box-sizing: border-box;
}

.login-card {
  width: 100%;
  background-color: #FFFFFF;
  border-radius: 20rpx;
  padding: 50rpx 40rpx;
  box-shadow: 0 10rpx 30rpx rgba(0, 0, 0, 0.05);
}

.login-header {
  text-align: center;
  margin-bottom: 60rpx;
}

.login-title {
  font-size: 40rpx;
  font-weight: bold;
  color: #333;
  margin-bottom: 16rpx;
}

.login-subtitle {
  font-size: 28rpx;
  color: #999;
}

.form-item {
  margin-bottom: 40rpx;
}

.form-label {
  font-size: 28rpx;
  color: #333;
  margin-bottom: 20rpx;
}

.input-wrapper {
  display: flex;
  align-items: center;
  background-color: #f5f7fa;
  border-radius: 10rpx;
  padding: 0 30rpx;
  height: 90rpx;
}

.icon {
  width: 36rpx;
  height: 36rpx;
  margin-right: 20rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 36rpx;
  color: #8e93f3;
}

.form-input {
  flex: 1;
  height: 90rpx;
  font-size: 28rpx;
  background: transparent;
  border: none;
}

.options-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 50rpx;
}

.remember-me {
  display: flex;
  align-items: center;
}

.checkbox {
  width: 32rpx;
  height: 32rpx;
  border: 2rpx solid #ddd;
  border-radius: 6rpx;
  margin-right: 16rpx;
  position: relative;
}

.checkbox.active {
  background-color: #b3b7ee;
  border-color: #b3b7ee;
}

.checkbox.active::after {
  content: "";
  position: absolute;
  top: 6rpx;
  left: 10rpx;
  width: 8rpx;
  height: 14rpx;
  border-right: 4rpx solid #fff;
  border-bottom: 4rpx solid #fff;
  transform: rotate(45deg);
}

.remember-text {
  font-size: 24rpx;
  color: #666;
}

.forgot-password {
  font-size: 24rpx;
  color: #999;
}

.login-button {
  width: 100%;
  height: 90rpx;
  background-color: #b3b7ee;
  color: #FFFFFF;
  border-radius: 10rpx;
  font-size: 32rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  margin-bottom: 40rpx;
}

.register-link {
  text-align: center;
  font-size: 24rpx;
  color: #666;
}

.register-text {
  color: #b3b7ee;
  margin-left: 10rpx;
}
</style> 