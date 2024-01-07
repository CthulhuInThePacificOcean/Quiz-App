<template>
  <form @submit.prevent>
    <input type="number" id="quantity" name="quantity" min="1" max="35" v-model="amount" />
    <button type="submit" @click="showAmount">Start Quiz</button>
  </form>
</template>

<script setup>
import { ref, defineEmits } from 'vue'

const amount = ref(1)
const link = ref('')
const questions = ''

const emit = defineEmits(['data'])

async function showAmount() {
  try {
    console.log(amount.value)
    const response = await fetch('https://the-trivia-api.com/v2/questions?limit=' + amount.value)

    if (!response.ok) {
      throw new Error('Network response was not ok')
    }

    const data = await response.json()
    console.log(data)
    link.value = data
    emit('data', link.value)
  } catch (error) {
    console.error('Error fetching data:', error)
  }
}
</script>
