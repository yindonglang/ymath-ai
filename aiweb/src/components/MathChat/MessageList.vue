<template>
  <div class="message-list">
    <MessageItem
      v-for="message in messages"
      :key="message.id"
      :message="message"
    />
  </div>
</template>

<script setup>
import MessageItem from './MessageItem.vue'

defineProps({
  messages: {
    type: Array,
    required: true
  }
})
</script>

<style scoped>
.message-list {
  flex: 1;
  overflow-y: auto;
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 12px;
}
</style>
