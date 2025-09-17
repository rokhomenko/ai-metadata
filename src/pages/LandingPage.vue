<template>
  <AppHeader
    :questionTop="questionTop"
    :resultsTop="resultsTop"
    :stepsTop="stepsTop"
  />

  <HeroSection ref="heroComp" />
  <QuestionSection ref="questionComp" />
  <ResultsSection ref="resultsComp" />
  <StepsSection ref="stepsComp" />
  <div class="cursor-circle">
    <span class="cursor-text"></span>
  </div>
</template>

<script setup>
  import { ref, onMounted, onBeforeUnmount, nextTick, defineExpose } from 'vue'
  import gsap from 'gsap'

  import AppHeader from '../components/AppHeader.vue'
  import HeroSection from '../components/HeroSection.vue'
  import QuestionSection from '../components/QuestionSection.vue'
  import ResultsSection from '../components/ResultsSection.vue'
  import StepsSection from '../components/StepsSection.vue'

  const heroComp = ref(null)
  const questionComp = ref(null)
  const resultsComp = ref(null)
  const stepsComp = ref(null)

  const questionTop = ref(0)
  const resultsTop = ref(0)
  const stepsTop = ref(0)

  const sectionRef = ref(null)
  defineExpose({ sectionRef })

  let xTo, yTo
  let resultsRect = null

  function globalMouseMove(e) {
    xTo && xTo(e.clientX)
    yTo && yTo(e.clientY)
  }

  let observer;

  onMounted(() => {
    nextTick(() => {
      setTimeout(() => {
        if (questionComp.value?.sectionRef) {
          questionTop.value = questionComp.value.sectionRef.offsetTop
        }
        if (resultsComp.value?.sectionRef) {
          resultsTop.value = resultsComp.value.sectionRef.offsetTop
        }
        if (stepsComp.value?.sectionRef) {
          stepsTop.value = stepsComp.value.sectionRef.offsetTop
        }

        const cursor = document.querySelector('.cursor-circle')
        const cursorText = cursor?.querySelector('.cursor-text')

        if (!cursor || !cursorText) {
          console.error('Cursor elements not found')
          return
        }

        const options = {
          root: null,
          rootMargin: '0px',
          threshold: 0.3
        };

        observer = new IntersectionObserver((entries) => {
          entries.forEach(entry => {
            if (entry.isIntersecting) {
              gsap.to(cursor, { width: 200, height: 200, duration: 0.4, ease: 'power3.out' });
              cursorText.textContent = "GET FORECAST";
              gsap.to(cursorText, { opacity: 1, duration: 0.3 });
            } else {
              gsap.to(cursor, { width: 20, height: 20, duration: 0.4, ease: 'power3.out' });
              gsap.to(cursorText, {
                opacity: 0,
                duration: 0.2,
                onComplete: () => (cursorText.textContent = "")
              });
            }
          });
        }, options);

        if (resultsComp.value?.sectionRef) {
          observer.observe(resultsComp.value.sectionRef);
        } else {
          console.error('ResultsSection sectionRef not found')
        }
      }, 100)
    })

    gsap.set(".cursor-circle", { xPercent: -50, yPercent: -50 })
    xTo = gsap.quickTo(".cursor-circle", "x", { duration: 0.28, ease: "power3" })
    yTo = gsap.quickTo(".cursor-circle", "y", { duration: 0.28, ease: "power3" })

    window.addEventListener("mousemove", globalMouseMove)
  })

  onBeforeUnmount(() => {
    window.removeEventListener("mousemove", globalMouseMove)
    if (observer) {
      observer.disconnect();
    }
  })
</script>

<style>
  .cursor-circle {
    height: 20px;
    width: 20px;
    background-color: #2E59E7;
    border-radius: 50%;
    position: fixed;
    top: 0;
    left: 0;
    pointer-events: none;
    z-index: 9999;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-size: 12px;
    font-weight: 600;
    text-align: center;
    line-height: 1;
  }

  .cursor-text {
    pointer-events: none;
    opacity: 0;
    white-space: nowrap;
  }
</style>
