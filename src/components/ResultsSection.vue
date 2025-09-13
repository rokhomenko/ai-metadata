<template>
  <section ref="sectionRef" class="h-screen bg-gray-900 flex items-center justify-center">
    <h1 class="text-white text-5xl font-bold">Results</h1>
  </section>
</template>

<script setup>
import { ref, defineExpose } from 'vue'

const sectionRef = ref(null)

defineExpose({
  sectionRef
})
</script>
