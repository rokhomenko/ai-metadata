<template>
  <section ref="sectionRef" class="h-screen flex items-center justify-center">
    <img :src="result" class="w-full"/>
  </section>
</template>

<script setup>
import { ref, defineExpose } from 'vue'
import result from '@/assets/result.png'

const sectionRef = ref(null)

defineExpose({
  sectionRef
})
</script>
