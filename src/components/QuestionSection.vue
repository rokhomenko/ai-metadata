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
        <div
          v-for="(card, idx) in cards"
          :key="idx"
          class="relative w-[322px] group"
        >
          <img :src="card.img" class="w-full" />
          <span
            v-if="card.label"
            class="absolute inset-0 z-50 flex items-center justify-center text-white font-semibold text-4xl"
          >
            {{ card.label }}
          </span>
          <div
            class="absolute bg-black h-0 w-[322px] top-[50%]
                   transition-all delay-100 duration-300 ease-in-out
                   opacity-0 group-hover:h-[350px] group-hover:opacity-100"
          >
            <div class="flex flex-col w-full p-10">
              <div class="text-white text-center font-regular">
                {{ card.description }}
              </div>
              <button
                class="sign-btn text-white bg-blue p-5 rounded-[10px] mt-7 mb-10 uppercase font-semibold"
              >
                Start for Free
              </button>
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
  import yes from '@/assets/yes.png'
  import no from '@/assets/no.png'
  import partially from '@/assets/partially.png'
  import arrow from '@/assets/arrow.svg'

  const sectionRef = ref(null)

  defineExpose({
    sectionRef
  })

  const cards = [
    {
      img: partially,
      label: 'Partially',
      description:
        "Awesome! Localizing your YouTube metadata is a perfect choice for you. Let's translate your video titles, descriptions, and tags, so people from all around the globe can discover your content."
    },
    {
      img: yes,
      label: 'Yes',
      description:
        "Awesome! Localizing your YouTube metadata is a perfect choice for you. Let's translate your video titles, descriptions, and tags, so people from all around the globe can discover your content."
    },
    {
      img: no,
      label: 'No',
      description:
        "Awesome! Localizing your YouTube metadata is a perfect choice for you. Let's translate your video titles, descriptions, and tags, so people from all around the globe can discover your content."
    }
  ]
</script>

<style scoped lang="scss">
  .sign-btn {
    position: relative;
    overflow: hidden;
    z-index: 1;
    transition: color 0.6s ease-in-out;

    &::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      z-index: -1;
      background-color: white;
      clip-path: circle(0% at 0% 100%);
      transition: clip-path 0.6s ease-in-out;
    }

    &:hover {
      color: #2E59E7;
      &::before {
        clip-path: circle(150% at 0% 100%);
      }
    }
  }
</style>