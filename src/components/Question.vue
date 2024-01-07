<template>
  <div>
    <h1 v-if="questions != undefined">{{ questions[index].question.text }}</h1>
    <h1 v-else>Wake Up</h1>
    <ul ref="answerList">
      <li
        v-for="(answer, aindex) in shuffledAnswers"
        :key="aindex"
        class="hover:text-blue-400"
        @click="answerClicked"
      >
        {{ answer }}
      </li>
    </ul>
    <div>
      <button @click="answerSubmit" v-if="answerSubmitted == false">Submit Answer</button>
      <button @click="nextQuestion" v-else>Next Question</button>
    </div>
  </div>
</template>

<script setup>
import { defineProps, ref, onMounted } from 'vue'

const index = ref(0)
const selected = ref(null)
const clicked = ref(false)
const answers = ref([])
const shuffledAnswers = ref([])
const correctAnswers = ref(0)
const answerList = ref(null)
const answerSubmitted = ref(false)

const props = defineProps({
  questions: {
    type: Array,
    required: true
  }
})

onMounted(() => {
  console.log('watch - questions changed')
  shuffleAnswers()
})

function nextQuestion() {
  if (index.value + 1 >= props.questions.length) {
    alert(`Quiz ended. You got ${correctAnswers.value} questions correct.`)
  } else {
    index.value += 1
    shuffleAnswers()
    answerSubmitted.value = false
    const listItems = answerList.value.children
    for (const item of listItems) {
      item.classList.remove('text-green-400')
      item.classList.remove('text-red-400')
    }
  }
}

function answerClicked(e) {
  const listItem = e.target
  const listItems = answerList.value.children
  for (const item of listItems) {
    item.classList.remove('text-blue-400')
  }
  listItem.classList.add('text-blue-400')
  selected.value = listItem.textContent.trim()
}

function answerSubmit() {
  const listItems = answerList.value.children
  if (selected.value == null) {
    alert('Please select an answer.')
    return
  }

  for (const item of listItems) {
    const isCorrectAnswer = item.textContent.trim() === props.questions[index.value].correctAnswer
    const isSelectedAnswer = item.textContent.trim() === selected.value

    if (isSelectedAnswer && isCorrectAnswer) {
      item.classList.add('text-green-400')
      correctAnswers.value += 1
    } else if (isSelectedAnswer) {
      item.classList.add('text-red-400')
    } else if (isCorrectAnswer) {
      item.classList.add('text-green-400')
    }

    item.classList.remove('text-blue-400')
  }

  answerSubmitted.value = true
}

function shuffleAnswers() {
  if (props.questions !== undefined && props.questions.length > 0) {
    if (index.value < props.questions.length) {
      const currentQuestion = props.questions[index.value]
      if (currentQuestion !== undefined) {
        const allAnswers = [currentQuestion.correctAnswer, ...currentQuestion.incorrectAnswers]
        shuffledAnswers.value = shuffleArray(allAnswers)
      } else {
        console.error('Current question is undefined.')
      }
    } else {
      console.error('Index is out of range.')
    }
  } else {
    console.error('No questions available.')
  }
}

function shuffleArray(array) {
  for (let i = array.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1))
    ;[array[i], array[j]] = [array[j], array[i]]
  }
  return array
}
</script>
