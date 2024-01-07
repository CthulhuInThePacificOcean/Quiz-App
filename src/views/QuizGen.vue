<template>
  <div>
    <select-amount @data="handleData" v-if="isQuestionInvisible" />
    <select-amount @data="handleData" v-else class="invisible" />
    <div>
      <question v-if="isQuestionInvisible" class="invisible" />
      <question v-else class="visible" :questions="questions" />
    </div>
  </div>
</template>

<script setup>
import SelectAmount from '@/components/SelectAmount.vue'
import Question from '@/components/Question.vue'
import { ref, defineEmits } from 'vue'
import { useRouter } from 'vue-router'

const emit = defineEmits(['data'])
const questions = ref([])
const router = useRouter()
const isQuestionInvisible = ref(true)

const handleData = (data) => {
  questions.value = data
  console.log(questions.value)
  isQuestionInvisible.value = false
}
</script>
