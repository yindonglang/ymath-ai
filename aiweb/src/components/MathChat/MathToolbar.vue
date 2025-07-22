<template>
  <div class="math-toolbar">
    <button 
      v-for="symbol in commonSymbols"
      :key="symbol.value"
      @click="insertSymbol(symbol.value)"
      :title="symbol.name"
      class="symbol-button"
    >
      {{ symbol.display }}
    </button>
  </div>
</template>

<script setup>
import { defineEmits } from 'vue'

const emit = defineEmits(['insert-symbol'])

const commonSymbols = [
  { name: 'Square Root', value: '\\sqrt{}', display: '√' },
  { name: 'Fraction', value: '\\frac{}{}', display: 'a/b' },
  { name: 'Summation', value: '\\sum_{}^{}', display: '∑' },
  { name: 'Integral', value: '\\int_{}^{}', display: '∫' },
  { name: 'Pi', value: '\\pi', display: 'π' },
  { name: 'Infinity', value: '\\infty', display: '∞' },
  { name: 'Greek Alpha', value: '\\alpha', display: 'α' },
  { name: 'Greek Beta', value: '\\beta', display: 'β' },
  { name: 'Equals', value: '=', display: '=' },
  { name: 'Not Equals', value: '\\neq', display: '≠' }
]

const insertSymbol = (symbol) => {
  emit('insert-symbol', symbol)
}
</script>

<style scoped>
.math-toolbar {
  display: flex;
  gap: 8px;
  padding: 8px 0;
  overflow-x: auto;
  scrollbar-width: none;
}

.math-toolbar::-webkit-scrollbar {
  display: none;
}

.symbol-button {
  background: white;
  border: 1px solid rgba(0,0,0,0.1);
  border-radius: 8px;
  padding: 6px 12px;
  font-family: 'KaTeX_Main', serif;
  cursor: pointer;
  transition: all 0.2s;
  white-space: nowrap;
}

.symbol-button:hover {
  background: var(--math-secondary);
  transform: translateY(-2px);
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
</style>
