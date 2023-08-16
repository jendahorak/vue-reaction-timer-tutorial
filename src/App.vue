<script setup>
// Imports
import Block from './components/Block.vue'
import Results from './components/Results.vue'
import { ref } from 'vue'
// Data
let isPlaying = ref(false)
let delay = ref(null)
let score = null
let position = undefined
let resultsShown = false

// Methods
const startRandomTime = () => {
  isPlaying.value = true
  delay = Math.random() * 2000
  resultsShown = false
}

const onEnd = (reactionTime) => {
  score = reactionTime
  isPlaying.value = false
  resultsShown = true
}
</script>

<template>
  <div class="play-board">
    <teleport to=".score-board">
      <h1>Reaction Timer</h1>
      <button class="custom-button" @click="startRandomTime" :disabled="isPlaying">Start</button>
      <Results v-if="resultsShown" :time="score"></Results>
    </teleport>
    <Block class="block" v-if="isPlaying" :delay="delay" @end="onEnd" />
  </div>
</template>

<style scoped>
h1 {
  cursor: default;
  user-select: none; /* Disable text selection */
}

.play-board {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 7rem;
}

.custom-button {
  background-color: var(--color-cyan);
  color: white;
  padding: 8px 24px;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin-top: 5px;
}

.custom-button:hover {
  background-color: #009e9b; /* Darker shade on hover */
}

.custom-button:disabled {
  background-color: #ccc; /* Change to the desired color for disabled state */
  cursor: default;
}
</style>
