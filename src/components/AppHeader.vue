<template>
  <header
    :class="[
      'fixed top-0 left-0 right-0 z-50 px-6 py-4 transition-all duration-400 ease-out, border-b-1 border-border',
      isDark ? 'bg-black text-white' : 'bg-white text-black'
    ]"
  >
    <div class="flex items-center justify-between border-b-">
      <div class="flex items-center space-x-3">
        <img :src="isDark ? logoWhite : logoBlack" class="h-10 w-auto transition-all duration-400 ease-out border-r-1 pr-3 border-border" />
        <img :src="isDark ? poweredWhite : poweredBlack" class="h-10 w-auto transition-all duration-400 ease-out" />
      </div>

      <div class="flex space-x-20">
        <nav class="flex items-center space-x-8">
          <a href="#about" class="text-sm font-medium hover:opacity-70 transition-opacity uppercase">About</a>
          <a href="#how" class="text-sm font-medium hover:opacity-70 transition-opacity uppercase">How it Works</a>
          <a href="#cases" class="text-sm font-medium hover:opacity-70 transition-opacity uppercase">Cases</a>
          <a href="#pricing" class="text-sm font-medium hover:opacity-70 transition-opacity uppercase">Pricing</a>
          <a href="#faq" class="text-sm font-medium hover:opacity-70 transition-opacity uppercase">FAQ</a>
        </nav>

        <div class="flex items-center space-x-4">
          <button
            class="text-sm font-medium hover:opacity-70 transition-opacity cursor-pointer uppercase"
          >
            Login
          </button>
          <button
            :class="[
              'sign-btn px-4 py-2 rounded text-sm font-medium uppercase cursor-pointer',
              isDark
                ? 'text-white border border-white'
                : 'text-black border border-black'
            ]"
          >
            Sign Up
          </button>
        </div>
      </div>
    </div>
  </header>
</template>

<script setup>
  import { ref, computed, onMounted, onUnmounted, watch } from 'vue'
  import logoBlack from '@/assets/logo-black.svg'
  import logoWhite from '@/assets/logo-white.svg'
  import poweredBlack from '@/assets/powered-black.svg'
  import poweredWhite from '@/assets/powered-white.svg'

  const props = defineProps({
    questionTop: Number,
    resultsTop: Number,
    stepsTop: Number
  })

  const headerState = ref('dark')
  const isDark = computed(() => headerState.value === 'dark')

  const updateHeaderState = () => {
    const scrollY = window.scrollY
    const questionThreshold = props.questionTop * 0.3

    if (scrollY >= props.stepsTop) {
      headerState.value = 'light'
    } else if (scrollY >= props.resultsTop) {
      headerState.value = 'dark'
    } else if (scrollY >= questionThreshold) {
      headerState.value = 'light'
    } else {
      headerState.value = 'dark'
    }
  }

  onMounted(() => {
    window.addEventListener('scroll', updateHeaderState)
  })

  onUnmounted(() => {
    window.removeEventListener('scroll', updateHeaderState)
  })

  watch(
    () => [props.questionTop, props.resultsTop, props.stepsTop],
    () => {
      updateHeaderState()
    },
    { immediate: true }
  )
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
      clip-path: circle(0% at 0% 100%);
      transition: clip-path 0.6s ease-in-out;
    }

    &:hover {
      &::before {
        clip-path: circle(150% at 0% 100%);
      }
    }
  }

  .sign-btn.border-white {
    color: white;
    &:hover {
      color: black;
    }
    &::before {
      background-color: white;
    }
  }

  .sign-btn.border-black {
    color: black;
    &:hover {
      color: white;
    }
    &::before {
      background-color: black;
    }
  }
</style>