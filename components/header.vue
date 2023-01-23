 <script setup lang="ts">
 import { ref } from 'vue'
 import { useIntervalFn } from '@vueuse/core'

 
 const greetings = ['Designer', 'Developer', 'Photographer', 'Artist']
const word = ref('Designer')
const interval = ref(1500)
let currentIndex = 0
const wordChanged = ref(false)
const { pause, resume, isActive } = useIntervalFn(() => {
  wordChanged.value = true
  setTimeout(() => { wordChanged.value = false }, 300)
  word.value = greetings[currentIndex]
  currentIndex = (currentIndex + 1) % greetings.length
}, interval)
</script>

<template>
    <h1>I AM A <span v-bind:class="{ 'animate': wordChanged }">{{ word }}</span></h1>
</template>
  
  
<style scoped>
  .animate {
    animation: changeWord 0.3s ease-in-out;
  }
  
  @keyframes changeWord {
    from { opacity: 0; }
    to { opacity: 1; }
  }
</style>
  