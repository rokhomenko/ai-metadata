<template>
  <div class="relative w-100 h-[33rem] bg-black rounded-full text-white overflow-hidden">
    <div class="absolute inset-0 flex items-center justify-center">
      <div class="text-center relative">
        <img :src="plus" />
        <img :src="people" class="absolute -top-[50px] -right-[30px]" />
      </div>
    </div>
    <div 
      class="absolute inset-0 flex items-center justify-center bg-black rounded-full overflow-hidden"
      :style="{ transform: `translateY(${step2TranslateY}%)` }"
    >
      <div class="text-center">
        <img :src="step2" class="absolute top-[60px] left-[85px]" />
      </div>
    </div>
    <div 
      class="absolute inset-0 flex items-center justify-center bg-black rounded-full overflow-hidden"
      :style="{ transform: `translateY(${step3TranslateY}%)` }"
    >
      <div class="text-center">
        <img :src="step3" />
      </div>
    </div>
  </div>
</template>

<script setup>
  import { computed } from 'vue';

  import plus from '@/assets/step1-plus.svg'
  import people from '@/assets/step1-people.svg'
  import step2 from '@/assets/step2.svg'
  import step3 from '@/assets/step3.svg'

  const props = defineProps({
    currentStep: {
      type: Number,
      required: true,
    },
    stepProgress: {
      type: Number,
      required: true,
    },
  });

  const step2TranslateY = computed(() => {
    if (props.currentStep < 1 || (props.currentStep === 1 && props.stepProgress === 0)) {
      return 100;
    }
    if (props.currentStep === 1) {
      return 100 - props.stepProgress * 100;
    }
    return 0;
  });

  const step3TranslateY = computed(() => {
    if (props.currentStep < 2) {
      return 100;
    }
    if (props.currentStep === 2) {
      return 100 - props.stepProgress * 100;
    }
    return 0;
  });
</script>
