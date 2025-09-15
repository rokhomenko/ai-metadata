<template>
  <section ref="sectionRef" class="h-screen flex justify-center">
    <img :src="result" class="w-full absolute z-1"/>
    <div class="flex flex-col z-2 text-white text-semibold w-2/3 mx-auto h-2/3 my-auto text-center">
        <div class="lx:text-[110px] lg:text-[80px] mt-10">
          Still Not Sure What Results Can You Expect?
        </div>
        <div class="lg:text-[22px] mt-10 xl:mt-30 mx-auto xl:w-[600px]">
          Find out how many views AI Metadata Translation can bring to your channel, and how much time it saves!
        </div>
    </div>
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
