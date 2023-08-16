<script setup>
import { onMounted, ref } from 'vue'

// DATA
const props = defineProps({
  delay: Number
})

let showBlock = ref(false)
let timer = null
let reactionTime = 0
let score = ref('')

// HOOKS
onMounted(() => {
  setTimeout(() => {
    showBlock.value = true
    startTimer()
  }, props.delay)
})

// Methods
const emit = defineEmits(['end'])

const startTimer = () => {
  timer = setInterval(() => {
    reactionTime += 10
  }, 10)
}

const endTimer = () => {
  clearInterval(timer)
  emit('end', reactionTime)
  showBlock.value = false
}
</script>

<template>
  <div class="block" v-if="showBlock" @click="endTimer"><span>Click me!</span></div>
</template>

<style scoped>
.block {
  max-width: 70%;
  background-color: var(--color-cyan);
  color: rgb(255, 255, 255);
  text-align: center;
  padding: 10%;
  border-radius: 20px;
  font-weight: 700;
  cursor: pointer;
  min-height: 7rem;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
