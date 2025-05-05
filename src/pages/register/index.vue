<template>
  <view class="register-container">
    <view class="register-card">
      <view class="register-header">
        <view class="register-title">账号注册</view>
        <view class="register-subtitle">创建您的新账号</view>
      </view>
      
      <view class="register-form">
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
            <text class="eye-icon" @tap="togglePasswordVisibility">
              {{ showPassword ? '👁' : '👁‍🗨' }}
            </text>
          </view>
        </view>
        
        <view class="form-item">
          <view class="form-label">确认密码</view>
          <view class="input-wrapper">
            <text class="icon">🔒</text>
            <input 
              class="form-input" 
              :type="showPassword ? 'text' : 'password'" 
              v-model="confirmPassword" 
              placeholder="请再次输入密码" 
            />
            <text class="eye-icon" @tap="togglePasswordVisibility">
              {{ showPassword ? '👁' : '👁‍🗨' }}
            </text>
          </view>
        </view>
        
        <button class="register-button" @tap="handleRegister">注 册</button>
        
        <view class="login-link">
          <text>已有账号？</text>
          <text class="login-text" @tap="goToLogin">立即登录</text>
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
const confirmPassword = ref('')
const showPassword = ref(false)

// 方法
const togglePasswordVisibility = () => {
  showPassword.value = !showPassword.value
}

const handleRegister = () => {
  if (!username.value || !password.value || !confirmPassword.value) {
    uni.showToast({
      title: '请填写完整注册信息',
      icon: 'none'
    })
    return
  }
  
  if (password.value !== confirmPassword.value) {
    uni.showToast({
      title: '两次输入的密码不一致',
      icon: 'none'
    })
    return
  }
  
  // 模拟注册请求
  uni.showLoading({ title: '注册中...' })
  
  setTimeout(() => {
    uni.hideLoading()
    uni.showToast({
      title: '注册成功',
      icon: 'success'
    })
    
    // 注册成功后跳转到首页
    setTimeout(() => {
      uni.switchTab({
        url: '/pages/index/index'
      })
    }, 1500)
  }, 1500)
}

const goToLogin = () => {
  uni.navigateBack()
}
</script>

<style lang="scss">
page {
  background-color: #b3b7ee;
  width: 100%;
  height: 100%;
}

.register-container {
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 30rpx;
  box-sizing: border-box;
}

.register-card {
  width: 100%;
  background-color: #FFFFFF;
  border-radius: 20rpx;
  padding: 50rpx 40rpx;
  box-shadow: 0 10rpx 30rpx rgba(0, 0, 0, 0.05);
}

.register-header {
  text-align: center;
  margin-bottom: 60rpx;
}

.register-title {
  font-size: 40rpx;
  font-weight: bold;
  color: #333;
  margin-bottom: 16rpx;
}

.register-subtitle {
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
  position: relative;
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

.register-button {
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

.login-link {
  text-align: center;
  font-size: 24rpx;
  color: #666;
}

.login-text {
  color: #b3b7ee;
  margin-left: 10rpx;
}

.eye-icon {
  position: absolute;
  right: 30rpx;
  color: #999;
  font-size: 40rpx;
}
</style>
