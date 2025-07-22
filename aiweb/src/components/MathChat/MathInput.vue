<template>
  <div class="math-input-container">
    <span class="function-f">F</span>
    <span class="bracket left">(</span>
    <textarea
      ref="textarea"
      v-model="inputText"
      @keydown.enter.exact.prevent="handleSend"
      @input="adjustHeight"
      placeholder="在这里打字跟F哥对话......"
      class="math-input"
    ></textarea>
    <span class="bracket right">)</span>
    <button @click="handleSend" class="send-button">
      =
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['send'])
const inputText = ref('')
const textarea = ref(null)

const adjustHeight = () => {
  const textareaEl = textarea.value
  textareaEl.style.height = 'auto'
  textareaEl.style.height = `${Math.min(textareaEl.scrollHeight, 120)}px`
}

const handleSend = () => {
  if (inputText.value.trim()) {
    emit('send', inputText.value)
    inputText.value = ''
    textarea.value.style.height = '40px'
  }
}

defineExpose({
  insertAtCursor: (symbol) => {
    const textareaEl = textarea.value
    const startPos = textareaEl.selectionStart
    const endPos = textareaEl.selectionEnd
    inputText.value = 
      inputText.value.substring(0, startPos) +
      symbol +
      inputText.value.substring(endPos)
    textareaEl.focus()
    textareaEl.setSelectionRange(startPos + symbol.length, startPos + symbol.length)
  }
})
</script>

<style scoped>
.math-input-container {
  display: flex;
  align-items: center;
  gap: 4px;
  background: #f0f2f5;
  border-radius: 24px;
  padding: 8px 16px;
  box-shadow: 0 1px 4px rgba(0,0,0,0.08);
}

.function-f {
  font-size: 24px;
  font-weight: bold;
  margin-right: 4px;
  color: var(--math-primary);
}

.bracket {
  font-size: 18px;
  font-weight: bold;
  color: var(--math-primary);
  height: 40px;
  display: flex;
  align-items: center;
}

.bracket.left {
  margin-right: 4px;
}

.bracket.right {
  margin-left: 4px;
}

.math-input {
  flex: 1;
  border: none;
  outline: none;
  resize: none;
  min-height: 40px;
  max-height: 120px;
  font-family: 'SF Pro Text', -apple-system, BlinkMacSystemFont, sans-serif;
  padding: 8px 0;
  background: rgba(255,255,255,0.7);
  border-radius: 12px;
  color: #333;
}

.send-button {
  background: var(--math-primary);
  color: white;
  border: none;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: transform 0.2s;
  font-size: 24px;
  font-weight: bold;
}

.send-button:hover {
  transform: scale(1.1);
}
</style>
