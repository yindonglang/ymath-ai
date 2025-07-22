<template>
  <div 
    class="message-item"
    :class="[message.sender, { 'has-math': containsMath(message.text) }]"
  >
    <div class="message-content" v-html="renderContent(message.text)"></div>
    <div class="message-time">
      {{ formatTime(message.timestamp) }}
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'
import katex from 'katex'
import 'katex/dist/katex.min.css'

const props = defineProps({
  message: {
    type: Object,
    required: true
  }
})

const containsMath = (text) => {
  return text.includes('$') || text.includes('\\(')
}

const renderContent = (text) => {
  // 渲染LaTeX公式
  return text.replace(/\$\$(.*?)\$\$|\$(.*?)\$|\\\((.*?)\\\)/g, (match, p1, p2, p3) => {
    const formula = p1 || p2 || p3
    try {
      return katex.renderToString(formula, {
        throwOnError: false,
        displayMode: !!p1
      })
    } catch {
      return match
    }
  })
}

const formatTime = (date) => {
  return new Date(date).toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
}
</script>

<style scoped>
.message-item {
  max-width: 80%;
  padding: 12px 16px;
  border-radius: 18px;
  position: relative;
  animation: fadeIn 0.3s ease-out;
}

.message-item.user {
  align-self: flex-end;
  background-color: var(--math-primary);
  color: white;
  border-bottom-right-radius: 4px;
}

.message-item:not(.user) {
  align-self: flex-start;
  background-color: var(--math-secondary);
  border-bottom-left-radius: 4px;
}

.has-math .message-content {
  font-family: "KaTeX_Main", "Times New Roman", serif;
}

.message-time {
  font-size: 0.75rem;
  opacity: 0.7;
  margin-top: 4px;
  text-align: right;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>
