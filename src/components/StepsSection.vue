<template>
  <section ref="sectionRef" class="h-screen bg-white flex items-center justify-center">
    <h1 class="text-black text-5xl font-bold">Steps</h1>
  </section>
</template>

<script setup>
import { ref, defineExpose } from 'vue'

const sectionRef = ref(null)

defineExpose({
  sectionRef
})
</script>
