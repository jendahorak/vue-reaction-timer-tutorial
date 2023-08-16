<script setup>
import { defineProps, onMounted, ref } from 'vue'
const props = defineProps({
  time: Number
})

// DATA

let rank = ref(null)

onMounted(() => {
  if (props.time < 250) {
    rank.value = '🔥 Coked up ? 🔥'
  } else if (props.time < 400) {
    rank.value = '⚡ Blazingly fast ⚡'
  } else if (props.time < 750) {
    rank.value = '😐 Average 😐'
  } else {
    rank.value = '🐢 Slow 🐢'
  }
})
</script>
<template>
  <div class="reaction-time">
    <h3>
      Your reaction time is:<span>{{ time }} ms</span>
    </h3>
    <h3>
      Your rank is: <span>{{ rank }}</span>
    </h3>
  </div>
</template>

<style scoped>
.reaction-time {
  margin-top: 5px;
}

.reaction-time h2 {
  margin: 0; /* Remove margin to ensure proper alignment */
}

.reaction-time span {
  color: var(--color-cyan);
  margin: 0; /* Remove margin to ensure proper alignment */
  margin-left: 10px; /* Add some spacing between h2 and p */
}
</style>
