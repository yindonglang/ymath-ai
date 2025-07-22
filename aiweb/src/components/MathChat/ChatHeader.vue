<template>
  <header class="chat-header">
    <div class="title">
      <span class="math-icon">F</span>
      <h1>数学F哥</h1>
    </div>
    <div class="subtitle">{{ randomSlogan }}</div>
  </header>
</template>

<script>
export default {
  data() {
    return {
      slogans: [
        'F哥，大家的亲哥！',
        'F哥的恩情还不完！',
        '有问题，找F哥！',
        '你说得对，但是F哥是一款由 Deepseek 驱动，隐冬狼负责提示词设计的开放式问答AI。',
        'F哥永远在进步！'
      ],
      randomSlogan: ''
    }
  },
  mounted() {
    this.randomSlogan = this.slogans[Math.floor(Math.random() * this.slogans.length)]
  }
}
</script>

<style scoped>
.chat-header {
  padding: 16px 20px;
  background: white;
  border-bottom: 1px solid rgba(0,0,0,0.08);
  text-align: center;
}

.title {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
}

.math-icon {
  background: var(--math-primary);
  color: white;
  width: 32px;
  height: 32px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
}

h1 {
  margin: 0;
  font-size: 1.5rem;
  font-weight: 600;
  color: var(--math-primary);
}

.subtitle {
  font-size: 0.875rem;
  color: rgba(0,0,0,0.6);
  margin-top: 4px;
}
</style>
