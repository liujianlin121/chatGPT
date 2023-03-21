<template>
  <view class="container">
    <scroll-view class="chat-box" scroll-y="true" :scroll-into-view="scrollIntoView" scroll-with-animation>
      <block v-for="(item, index) in messages" :key="index">
        <view class="message-item" :class="item.type === 'send' ? 'send' : 'receive'">
          <image class="avatar" :src="item.avatar" mode="aspectFill"></image>
          <view class="message-content">
            <text class="message-text">{{item.content}}</text>
          </view>
        </view>
      </block>
      <view class="scroll-placeholder"></view>
    </scroll-view>
    <view class="input-box">
      <input class="input" placeholder="请输入消息" :value="inputValue" @input="onInput"></input>
      <button class="send-btn" @click="sendMessage">发送</button>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      messages: [], // 消息列表
      inputValue: '', // 输入框的值
      scrollIntoView: '', // 滚动到的位置
    }
  },
  methods: {
    // 发送消息
    sendMessage() {
      if (!this.inputValue) return
      this.messages.push({
        type: 'send',
        avatar: '发送方头像地址',
        content: this.inputValue,
      })
      this.inputValue = ''
      this.scrollIntoView = `msg-${this.messages.length - 1}`
    },
    // 输入框输入
    onInput(e) {
      this.inputValue = e.detail.value
    },
  },
}
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  height: 100%;
}
.chat-box {
  flex: 1;
  padding: 20rpx;
}
.message-item {
  display: flex;
  align-items: flex-end;
  margin-bottom: 20rpx;
}
.message-item.send {
  justify-content: flex-end;
}
.avatar {
  width: 50rpx;
  height: 50rpx;
  border-radius: 50%;
  margin-right: 10rpx;
}
.message-content {
  max-width: 60%;
  background-color: #eee;
  border-radius: 10rpx;
  padding: 10rpx;
}
.message-text {
  font-size: 28rpx;
}
.input-box {
  display: flex;
  align-items: center;
  background-color: #fff;
  padding: 20rpx;
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
}
.input {
  flex: 1;
  height: 60rpx;
  border: none;
  background-color: #eee;
  border-radius: 30rpx;
  padding: 0 20rpx;
  font-size: 28rpx;
}
.send-btn {
  margin-left: 20rpx;
  width: 120rpx;
  height: 60rpx;
  border: none;
  background-color: #007aff;
  border-radius: 30rpx;
  color: #fff;
  font-size: 28rpx;
}
.scroll-placeholder {
  height: 60rpx;
}
</style>
