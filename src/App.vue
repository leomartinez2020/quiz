<template>
  <div id="app" class="flex flex-col items-center justify-center min-h-screen bg-gray-100 p-4">
    <QuestionDisplay :question="currentQuestion" />
    <NextButton @click="getNextQuestion" />
    <PreviousButton @click="getPreviousQuestion" />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import QuestionDisplay from './components/QuestionDisplay.vue'
import NextButton from './components/NextButton.vue'
import PreviousButton from './components/PreviousButton.vue'

//import questionsData from './questions.json'
import questionsData from './translations.json'

const questions = questionsData.questions

const currentQuestionIndex = ref(0)

const currentQuestion = computed(() => questions[currentQuestionIndex.value])

const getNextQuestion = () => {
  currentQuestionIndex.value = (currentQuestionIndex.value + 1) % questions.length
}

const getPreviousQuestion = () => {
  currentQuestionIndex.value = (currentQuestionIndex.value - 1) % questions.length
}

</script>
