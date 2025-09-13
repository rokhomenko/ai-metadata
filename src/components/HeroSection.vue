<template>
  <section ref="sectionRef" class="h-screen flex items-center justify-center bg-black">
    <div class="relative w-full h-[400px]">
      <div class="relative z-10">
        <h1 class="text-white">111</h1>  
      </div>
      <img :src="polygon" />
      
    </div>
  </section>
  <div class="bg-white z-20">
    <img :src="pixels" />
  </div>
</template>

<script setup>
import { ref, defineExpose } from 'vue'
import polygon from '@/assets/polygons.png'
import pixels from '@/assets/hero-pixels.jpg'

const sectionRef = ref(null)

defineExpose({
  sectionRef
})
</script>
