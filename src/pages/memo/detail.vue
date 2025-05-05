<template>
  <view class="memo-detail-container">
    <view class="memo-detail-card">
      <view class="card-header">
        <view class="header-row">
          <view class="title-area">
            <text v-if="!editMode" class="card-title">{{memo.title}}</text>
            <input v-else v-model="memo.title" class="edit-title-input" />
          </view>
          <view class="action-btns">
            <view v-if="!editMode" class="edit-btn" @tap="toggleEdit"><text>✏️</text></view>
            <view v-if="editMode" class="save-btn" @tap="saveChanges"><text>✔️</text></view>
            <view v-if="editMode" class="cancel-btn" @tap="cancelEdit"><text>✖️</text></view>
            <view class="delete-btn" @tap="deleteMemo"><text>🗑️</text></view>
            <view class="close-btn" @tap="closeMemo"><text class="close-icon">×</text></view>
          </view>
        </view>
      </view>
      
      <view class="card-content">
        <text v-if="!editMode" class="content-text">{{memo.content}}</text>
        <textarea v-else v-model="memo.content" class="edit-content-textarea" auto-height maxlength="5000"></textarea>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      memoId: null,
      memo: {
        title: '',
        content: ''
      },
      editMode: false
    }
  },
  onLoad(option) {
    if (option.id) {
      this.memoId = option.id;
      this.loadMemoData(option.id);
    }
  },
  methods: {
    loadMemoData(id) {
      // 从本地存储加载数据
      const list = uni.getStorageSync('memoList') || [];
      const found = list.find(item => String(item.id) === String(id));
      if (found) {
        this.memo = found;
      } else {
        this.memo = { title: '未找到', content: '未找到该备忘录内容' };
      }
    },
    closeMemo() {
      uni.navigateBack();
    },
    toggleEdit() {
      this.editMode = true;
    },
    saveChanges() {
      let list = uni.getStorageSync('memoList') || [];
      const idx = list.findIndex(item => String(item.id) === String(this.memoId));
      if (idx !== -1) {
        list[idx] = { id: this.memoId, title: this.memo.title, content: this.memo.content };
        uni.setStorageSync('memoList', list);
        uni.showToast({ title: '保存成功', icon: 'success', duration: 800 });
        this.editMode = false;
      }
    },
    cancelEdit() {
      this.loadMemoData(this.memoId);
      this.editMode = false;
    },
    deleteMemo() {
      uni.showModal({
        title: '删除',
        content: '确认删除该备忘录？',
        success: (res) => {
          if (res.confirm) {
            let list = uni.getStorageSync('memoList') || [];
            list = list.filter(item => String(item.id) !== String(this.memoId));
            uni.setStorageSync('memoList', list);
            uni.showToast({ title: '删除成功', icon: 'success', duration: 800 });
            setTimeout(() => { uni.navigateBack(); }, 800);
          }
        }
      });
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

.memo-detail-container {
  width: 100%;
  min-height: 100vh;
  padding: 40rpx 30rpx;
  box-sizing: border-box;
}

.memo-detail-card {
  width: 100%;
  background-color: #FFFFFF;
  border-radius: 20rpx;
  box-shadow: 0 8rpx 24rpx rgba(0, 0, 0, 0.08);
  overflow: hidden;
  position: relative;
  padding: 40rpx;
  box-sizing: border-box;
  min-height: 90vh;
}

.card-header {
  position: relative;
  margin-bottom: 40rpx;
  padding-right: 40rpx;
}

.header-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.title-area {
  flex: 1;
}

.card-title {
  font-size: 36rpx;
  font-weight: bold;
  color: #333;
  line-height: 1.4;
}

.edit-title-input {
  font-size: 36rpx;
  font-weight: bold;
  color: #333;
  line-height: 1.4;
  padding: 10rpx;
  border: 1rpx solid #ccc;
  border-radius: 10rpx;
}

.action-btns {
  display: flex;
  align-items: center;
}

.edit-btn, .save-btn, .cancel-btn, .delete-btn, .close-btn {
  margin-left: 20rpx;
  padding: 10rpx;
  border-radius: 10rpx;
  display: flex;
  justify-content: center;
  align-items: center;
}

.edit-btn {
  background-color: #4CAF50;
  color: #fff;
}

.save-btn {
  background-color: #03A9F4;
  color: #fff;
}

.cancel-btn {
  background-color: #FF9800;
  color: #fff;
}

.delete-btn {
  background-color: #F44336;
  color: #fff;
}

.close-btn {
  background-color: #999;
  color: #fff;
}

.close-icon {
  font-size: 48rpx;
  color: #999;
  font-weight: 300;
}

.card-content {
  padding-bottom: 40rpx;
}

.content-text {
  font-size: 28rpx;
  color: #666;
  line-height: 1.6;
  white-space: pre-wrap;
}

.edit-content-textarea {
  font-size: 28rpx;
  color: #666;
  line-height: 1.6;
  padding: 10rpx;
  border: 1rpx solid #ccc;
  border-radius: 10rpx;
}
</style>