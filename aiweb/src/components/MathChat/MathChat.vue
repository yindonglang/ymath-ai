<template>
  <div class="math-chat-container">
    <ChatHeader />
    <MessageList :messages="messages" />
    <div class="input-area">
      <MathInput @send="handleSend" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import ChatHeader from './ChatHeader.vue'
import MessageList from './MessageList.vue'
import MathInput from './MathInput.vue'

const messages = ref([])

const handleSend = (text) => {
  messages.value.push({
    id: Date.now(),
    text,
    sender: 'user',
    timestamp: new Date()
  })
}

const insertSymbol = (symbol) => {
  // 将由MathInput组件处理
}
</script>

<style scoped>
.math-chat-container {
  display: flex;
  flex-direction: column;
  height: 100vh;
  background: linear-gradient(135deg, #f5f7fa 0%, #e4e8eb 100%);
  font-family: 'SF Pro Display', -apple-system, BlinkMacSystemFont, sans-serif;
}
.input-area {
  padding: 16px;
  background: white;
  border-top: 1px solid rgba(0,0,0,0.08);
}
</style>
