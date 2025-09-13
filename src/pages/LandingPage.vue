<template>
  <AppHeader
    :questionTop="questionTop"
    :resultsTop="resultsTop"
    :stepsTop="stepsTop"
  />

  <HeroSection ref="heroComp" />
  <QuestionSection ref="questionComp" />
  <ResultsSection ref="resultsComp" />
  <StepsSection ref="stepsComp" />
</template>

<script setup>
import { ref, onMounted, nextTick } from 'vue'
import AppHeader from '../components/AppHeader.vue'
import HeroSection from '../components/HeroSection.vue'
import QuestionSection from '../components/QuestionSection.vue'
import ResultsSection from '../components/ResultsSection.vue'
import StepsSection from '../components/StepsSection.vue'

const heroComp = ref(null)
const questionComp = ref(null)
const resultsComp = ref(null)
const stepsComp = ref(null)

const questionTop = ref(0)
const resultsTop = ref(0)
const stepsTop = ref(0)

onMounted(() => {
  nextTick(() => {
    questionTop.value = questionComp.value.sectionRef.offsetTop
    resultsTop.value = resultsComp.value.sectionRef.offsetTop
    stepsTop.value = stepsComp.value.sectionRef.offsetTop
  })
})
</script>
