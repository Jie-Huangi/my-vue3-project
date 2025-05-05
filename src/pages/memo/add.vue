<template>
  <view class="memo-add-container">
    <view class="memo-add-card">
      <view class="card-header">
        <text class="card-title">新增备忘录</text>
        <view class="close-btn" @tap="cancelAdd">
          <text class="close-icon">×</text>
        </view>
      </view>
      
      <view class="form-content">
        <view class="form-item">
          <view class="form-label">标题</view>
          <input 
            class="title-input" 
            type="text" 
            v-model="memo.title" 
            placeholder="请输入标题" 
            maxlength="50"
          />
        </view>
        
        <view class="form-item">
          <view class="form-label">内容</view>
          <textarea 
            class="content-textarea" 
            v-model="memo.content" 
            placeholder="请输入内容" 
            maxlength="5000"
            auto-height
          />
        </view>
      </view>
      
      <view class="form-footer">
        <button class="cancel-btn" @tap="cancelAdd">取消</button>
        <button class="save-btn" @tap="saveMemo">保存</button>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      memo: {
        title: '',
        content: ''
      }
    }
  },
  methods: {
    saveMemo() {
      if (!this.memo.title.trim()) {
        uni.showToast({
          title: '请输入标题',
          icon: 'none'
        });
        return;
      }
      // 保存到本地存储
      let list = uni.getStorageSync('memoList') || [];
      // 生成唯一id
      const newId = Date.now();
      const newMemo = {
        id: newId,
        title: this.memo.title,
        content: this.memo.content
      };
      list.unshift(newMemo);
      uni.setStorageSync('memoList', list);
      uni.showToast({
        title: '保存成功',
        icon: 'success',
        duration: 800
      });
      setTimeout(() => {
        uni.navigateBack();
      }, 800);
    },
    cancelAdd() {
      uni.navigateBack();
    }
  }
}
</script>

<style lang="scss">
page {
  background-color: #b3b7ee;
  width: 100%;
  height: 100%;
}

.memo-add-container {
  width: 100%;
  min-height: 100vh;
  padding: 40rpx 30rpx;
  box-sizing: border-box;
}

.memo-add-card {
  width: 100%;
  background-color: #FFFFFF;
  border-radius: 20rpx;
  box-shadow: 0 8rpx 24rpx rgba(0, 0, 0, 0.08);
  overflow: hidden;
  position: relative;
  padding: 40rpx;
  box-sizing: border-box;
  min-height: 90vh;
  display: flex;
  flex-direction: column;
}

.card-header {
  position: relative;
  margin-bottom: 40rpx;
  padding-right: 40rpx;
}

.card-title {
  font-size: 36rpx;
  font-weight: bold;
  color: #333;
  line-height: 1.4;
}

.close-btn {
  position: absolute;
  right: -20rpx;
  top: -10rpx;
  width: 60rpx;
  height: 60rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
}

.close-icon {
  font-size: 48rpx;
  color: #999;
  font-weight: 300;
}

.form-content {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.form-item {
  margin-bottom: 30rpx;
}

.form-label {
  font-size: 28rpx;
  color: #333;
  margin-bottom: 20rpx;
}

.title-input {
  width: 100%;
  height: 90rpx;
  background-color: #f5f7fa;
  border-radius: 10rpx;
  padding: 0 30rpx;
  box-sizing: border-box;
  font-size: 28rpx;
}

.content-textarea {
  width: 100%;
  min-height: 400rpx;
  background-color: #f5f7fa;
  border-radius: 10rpx;
  padding: 20rpx 30rpx;
  box-sizing: border-box;
  font-size: 28rpx;
  line-height: 1.6;
}

.form-footer {
  margin-top: auto;
  padding-top: 40rpx;
  display: flex;
  justify-content: flex-end;
}

.cancel-btn, .save-btn {
  height: 80rpx;
  border-radius: 10rpx;
  font-size: 28rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 60rpx;
  margin-left: 20rpx;
}

.cancel-btn {
  background-color: #f5f5f5;
  color: #666;
}

.save-btn {
  background-color: #b3b7ee;
  color: #FFFFFF;
}
</style> 