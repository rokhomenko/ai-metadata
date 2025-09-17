<template>
  <section ref="sectionRef" class="relative bg-white text-black py-24">
    <div class="container mx-auto grid grid-cols-2 gap-16 h-full">
      <div class="relative">
        <div class="progress absolute left-15 w-1 h-full bg-gray-200"></div>
        <div 
          class="progress-blue absolute left-15 w-1 bg-blue-600"
          :style="{ height: progressBarHeight + '%' }"
        >
        </div>
        <div class="ml-8 steps">
          <div v-for="step in steps" :key="step.id" class="step-item relative ml-[100px]">
            <div class="flex flex-col items-start gap-6">
              <div class="flex items-center justify-center w-10 h-10 border border-black rounded-full">
                <span class="text-sm font-medium">{{ step.id }}</span>
              </div>
              <div>
                <h2 class="text-[56px] font-bold mb-2 leading-snug">
                  {{ step.title }}
                </h2>
                <p class="text-black text-base leading-relaxed mt-10 w-[70%]">
                  {{ step.description }}
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="sticky top-0 h-screen flex items-center justify-center">
        <StepVisuals :current-step="currentStep" :step-progress="stepProgress" />
      </div>
    </div>
  </section>
</template>

<script setup>
  import { ref, onMounted, onBeforeUnmount } from 'vue';
  import StepVisuals from './StepVisuals.vue';

  const steps = ref([
    { id: 1, title: 'Connect Your Channel', description: "Link your channel to AIR Media-Tech with just a few clicks. It's an ultimate space for creators with over 30 tailored services, including AI Metadata translation." },
    { id: 2, title: 'Get Translations', description: "AI Metadata Translation analyzes your channel, generates translations in minutes, and adds them to your channel automatically." },
    { id: 3, title: 'Monitor Growth', description: "Watch your channel's global views grow! After adding metadata in new languages, you’ll see your content reaching new countries along with boosting your income." },
  ]);

  const sectionRef = ref(null);

  defineExpose({ sectionRef });

  const progressBarHeight = ref(0);
  const currentStep = ref(1);
  const stepProgress = ref(0);

  const handleScroll = () => {
    if (!sectionRef.value) return;

    const rect = sectionRef.value.getBoundingClientRect();
    const scrollTop = window.scrollY - sectionRef.value.offsetTop;
    const scrollHeight = rect.height - window.innerHeight;

    if (scrollTop < 0) {
      progressBarHeight.value = 0;
      currentStep.value = 1;
      stepProgress.value = 0;
      return;
    }

    const totalProgress = Math.min(Math.max(scrollTop / scrollHeight, 0), 1);
    
    progressBarHeight.value = totalProgress * 100;

    const stepCount = steps.value.length;
    const progressPerStep = 1 / (stepCount - 1);

    const currentStepIndex = Math.floor(totalProgress / progressPerStep);
    currentStep.value = currentStepIndex + 1;

    const progressInCurrentStep = (totalProgress - (currentStepIndex * progressPerStep)) / progressPerStep;
    stepProgress.value = isNaN(progressInCurrentStep) ? 0 : progressInCurrentStep;
  };

  onMounted(() => {
    window.addEventListener('scroll', handleScroll);
    handleScroll();
  });

  onBeforeUnmount(() => {
    window.removeEventListener('scroll', handleScroll);
  });
</script>

<style scoped lang="scss">
  .progress,
  .progress-blue {
    top: 20vh;
  }

  .steps {
    margin-top: 20vh;

    .step-item {
      margin-bottom: 30vh;

      &:first-child {
        padding-top: 0;
      }
    }
  }
</style>