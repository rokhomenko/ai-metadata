<template>
  <section ref="sectionRef" class="relative z-20 h-screen bg-white flex items-center justify-center">
    <img :src="bullhorn" />
  </section>
</template>

<script setup>
import { ref, defineExpose } from 'vue'
import bullhorn from '@/assets/Bullhorn.svg'

const sectionRef = ref(null)

defineExpose({
  sectionRef
})
</script>
