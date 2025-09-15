<template>
  <section ref="sectionRef" class="relative z-20 bg-white w-full">
    <div class="flex flex-col items-center justify-center">
      <img :src="bullhorn" class="w-[200px] h-[200px] mt-30" />
      <div class="flex max-w-2xl leading-normal text-center text-[54px] font-semibold mt-5">
        Are your videos understandable without voice narration
      </div>
      <div class="font-semibold text-[30px] mt-5">Choose answear</div>
      <img :src="arrow" class="mt-3 mb-20" />
      <div class="flex flex-row gap-25 flex-wrap mb-80">
        <div class="relative w-[322px] group">
          <img :src="partially"/>
          <div class="absolute bg-black h-0 w-[322px] top-[60%]
                       transition-all delay-100 duration-300 ease-in-out
                       opacity-0 group-hover:h-[350px] group-hover:opacity-100">
            <div class="flex flex-col w-full p-10">
              <div class="text-white text-center font-regular">
                Awesome! Localizing your YouTube metadata is a perfect choice for you. Let's translate your video titles, descriptions, and tags, so people from all around the globe can discover your content.
              </div>
              <button class="text-white bg-blue p-5 rounded-[10px] mt-7 mb-10 uppercase font-semibold">Start for Free</button>
            </div>
          </div>
        </div>
        <div class="relative w-[322px] group">
          <img :src="yes" class="absolute"/>
          <div class="absolute bg-black h-0 w-[322px] top-[60%]
                       transition-all delay-100 duration-300 ease-in-out
                       opacity-0 group-hover:h-[350px] group-hover:opacity-100">
            <div class="flex flex-col w-full p-10">
              <div class="text-white text-center font-regular">
                Awesome! Localizing your YouTube metadata is a perfect choice for you. Let's translate your video titles, descriptions, and tags, so people from all around the globe can discover your content.
              </div>
              <button class="text-white bg-blue p-5 rounded-[10px] mt-7 mb-10 uppercase font-semibold">Start for Free</button>
            </div>
          </div>
        </div>
        <div class="relative w-[322px] group">
          <img :src="no" class="absolute"/>
          <div class="absolute bg-black h-0 w-[322px] top-[60%]
                       transition-all delay-100 duration-300 ease-in-out
                       opacity-0 group-hover:h-[350px] group-hover:opacity-100">
            <div class="flex flex-col w-full p-10">
              <div class="text-white text-center font-regular">
                Awesome! Localizing your YouTube metadata is a perfect choice for you. Let's translate your video titles, descriptions, and tags, so people from all around the globe can discover your content.
              </div>
              <button class="text-white bg-blue p-5 rounded-[10px] mt-7 mb-10 uppercase font-semibold">Start for Free</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, defineExpose } from 'vue'
import bullhorn from '@/assets/Bullhorn.svg'
import yes from '@/assets/yes.svg'
import no from '@/assets/no.svg'
import partially from '@/assets/partially.svg'
import arrow from '@/assets/arrow.svg'

const sectionRef = ref(null)

defineExpose({
  sectionRef
})
</script>
