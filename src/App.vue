<template>
  <div id="app" class="flex flex-col items-center justify-center min-h-screen bg-gray-100 p-4">
    <div class="mb-6 w-full max-w-md">
      <label for="file-select" class="block text-sm font-medium text-gray-700 mb-1">Choose a question set:</label>
      <select
        id="file-select"
        v-model="selectedFile"
        class="w-full border border-gray-300 rounded-lg px-3 py-2 bg-white shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-400 text-base"
      >
        <option v-for="file in fileOptions" :key="file.value" :value="file.value">{{ file.label }}</option>
      </select>
    </div>
    <QuestionDisplay :question="currentQuestion" />
    <NextButton @click="getNextQuestion" />
    <PreviousButton @click="getPreviousQuestion" />
    <p class="mt-4 text-sm text-gray-500">{{ currentQuestionIndex + 1 }} / {{ questions.length }}</p>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue'
import QuestionDisplay from './components/QuestionDisplay.vue'
import NextButton from './components/NextButton.vue'
import PreviousButton from './components/PreviousButton.vue'

import brainersData from './brainers.json'
import cognatesData from './cognates.json'
import incompleteSentencesData from './incomplete_sentences.json'
import metooData from './metoo.json'
import phraalsData from './phrasals.json'
import preguntasData from './preguntas.json'
import questionsData from './questions.json'
import reportedSpeechData from './reportedspeech.json'
import translationsData from './translations.json'
import writingData from './writing.json'
import yesnoQuestions1 from './yesno1.json'
import yesnoQuestions2 from './yesno2.json'

const fileOptions = [
  { value: 'preguntas', label: 'Preguntas' },
  { value: 'brainers', label: 'Brainers' },
  { value: 'cognates', label: 'Cognates' },
  { value: 'incomplete_sentences', label: 'Incomplete Sentences' },
  { value: 'metoo', label: 'Me Too' },
  { value: 'phrasals', label: 'Phrasals' },
  { value: 'questions', label: 'Questions' },
  { value: 'reportedspeech', label: 'Reported Speech' },
  { value: 'translations', label: 'Translations' },
  { value: 'writing', label: 'Writing' },
  { value: 'yesno1', label: 'YesNoQuestions1' },
  { value: 'yesno2', label: 'YesNoQuestions2' },
]

const allData = {
  brainers: brainersData.questions,
  cognates: cognatesData.questions,
  incomplete_sentences: incompleteSentencesData.questions,
  metoo: metooData.questions,
  phrasals: phraalsData.questions,
  preguntas: preguntasData.questions,
  questions: questionsData.questions,
  reportedspeech: reportedSpeechData.questions,
  translations: translationsData.questions,
  writing: writingData.questions,
  yesno1: yesnoQuestions1.questions,
  yesno2: yesnoQuestions2.questions,
}

const selectedFile = ref('preguntas')
const currentQuestionIndex = ref(0)

const questions = computed(() => allData[selectedFile.value])
const currentQuestion = computed(() => questions.value[currentQuestionIndex.value])

watch(selectedFile, () => {
  currentQuestionIndex.value = 0
})

const getNextQuestion = () => {
  currentQuestionIndex.value = (currentQuestionIndex.value + 1) % questions.value.length
}

const getPreviousQuestion = () => {
  currentQuestionIndex.value = (currentQuestionIndex.value - 1 + questions.value.length) % questions.value.length
}
</script>
