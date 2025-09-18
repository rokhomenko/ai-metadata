<template>
  <section ref="sectionRef" class="h-screen flex items-center justify-center bg-black">
    <img :src="polygon" 
       alt="polygon" 
       class="absolute -top-40 left-0 w-full h-auto z-0 hidden sm:block" />
    <div class="relative w-full mt-50 p-5 sm:p-10 md:p-15 2xl:p-30 3xl:p-50">
      <div class="grid grid-cols-1 gap-2 md:grid-cols-4 md:grid-rows-4 md:gap-0 items-center">
        <div class="order-1 md:col-span-2 md:row-start-1 md:row-end-2
                    hero-title">
          AI YouTube 
        </div>
        <div class="order-2 md:col-start-2 md:col-end-4 md:row-start-2 md:row-end-3 hero-title">
          Metadata 
        </div>
        <div class="order-3 md:col-span-2 md:row-start-3 md:row-end-4 hero-title">
          Translation
        </div>
        <div class="order-4 lg:col-start-3 lg:col-end-4 lg:row-start-3 lg:row-end-4
                    md:col-start-1 md:col-end-5 md:row-start-4 md:row-end-5 xl:w-[70%] hero-description">
          Take Your YouTube Content Global by Localizing Your YouTube Metadata.
        </div>
        <div class="order-5 md:col-start-1 md:col-end-2 md:row-start-2 md:row-end-3
                  text-white font-display font-semibold flex items-center">
          <button class="button">
            <span class="uppercase">what is this?</span>
            <span class="circle">
              <span class="inner">
                <img :src="play" />
              </span>
            </span>
          </button>
        </div>
        <div 
          ref="order6Ref"
          class="order-6 md:col-start-4 md:col-end-5 md:row-start-3 md:row-end-5 h-full z-50 flex justify-center items-center relative"
        >
          <div 
            ref="tryBtnRef"
            class="flex bg-blue text-white rounded-full h-45 w-45 justify-center items-center hover:cursor-pointer"
            style="will-change: transform;"
          >
            TRY FOR FREE
          </div>
        </div>
      </div>
    </div>
  </section>
  <div class="relative bg-white z-20">
    <img :src="pixels" class="w-full" />
  </div>
</template>

<script setup>
  import { ref, onMounted, onBeforeUnmount, defineExpose } from 'vue'
  import gsap from 'gsap'

  import polygon from '@/assets/polygons.png'
  import pixels from '@/assets/hero-pixels.png'
  import play from '@/assets/play.svg'

  const sectionRef = ref(null)
  const order6Ref = ref(null)
  const tryBtnRef = ref(null)

  let xToBtn, yToBtn

  function order6MouseMove(e) {
    const container = order6Ref.value
    const btn = tryBtnRef.value
    if (!container || !btn) return

    const rect = container.getBoundingClientRect()
    const btnRect = btn.getBoundingClientRect()

    const x = e.clientX - rect.left
    const y = e.clientY - rect.top

    const offsetX = x - rect.width / 2
    const offsetY = y - rect.height / 2

    const factor = 0.35

    const maxX = Math.max(8, (rect.width - btnRect.width) / 2)
    const maxY = Math.max(8, (rect.height - btnRect.height) / 2)

    let targetX = Math.max(-maxX, Math.min(maxX, offsetX * factor))
    let targetY = Math.max(-maxY, Math.min(maxY, offsetY * factor))

    xToBtn && xToBtn(targetX)
    yToBtn && yToBtn(targetY)
  }

  function order6MouseLeave() {
    const btn = tryBtnRef.value
    if (!btn) return
    gsap.to(btn, { x: 0, y: 0, duration: 0.8, ease: 'elastic.out(1, 0.45)' })
  }

  onMounted(() => {
    const container = order6Ref.value
    const btn = tryBtnRef.value
    if (container && btn) {
      gsap.set(btn, { x: 0, y: 0 })
      xToBtn = gsap.quickTo(btn, "x", { duration: 0.6, ease: "power3.out" })
      yToBtn = gsap.quickTo(btn, "y", { duration: 0.6, ease: "power3.out" })

      container.addEventListener('pointermove', order6MouseMove)
      container.addEventListener('pointerleave', order6MouseLeave)
    }
  })

  onBeforeUnmount(() => {
    const container = order6Ref.value
    if (container) {
      container.removeEventListener('pointermove', order6MouseMove)
      container.removeEventListener('pointerleave', order6MouseLeave)
    }
  })
</script>

<style lang="scss">
  .button {
    display: flex;
    justify-content: space-around;
    align-items: center;
    width: 270px;
    height: 85px;
    position: relative;
    padding: 10px 20px;
    background: transparent;
    border: 2px solid transparent;
    border-radius: 8px;
    z-index: 0;
    font-size: 40;
    cursor: pointer;

    span {
      color: white;
    }

    &::before {
      content: '';
      position: absolute;
      inset: 0;
      border-radius: 8px;
      padding: 2px;
      background: linear-gradient(45deg, #FFFFFF, #FD86FF, #FB38FF, #3858FF, #8BFF78);
      -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
      -webkit-mask-composite: destination-out;
      mask-composite: exclude;
      z-index: -1;
    }

    &:hover {
      transform: scale(1.1);

      &::before {
        background-position: 100% 100%;
        background-size: 300% 300%;
      }
    }
  }

  .circle {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  position: relative;
  padding: 2px;
  background: linear-gradient(45deg, #FFFFFF, #FD86FF, #FB38FF, #3858FF, #8BFF78);
  cursor: pointer;
  transition: transform 0.3s;

  &::before {
    content: "";
    position: absolute;
    inset: 2px;
    background: black;
    border-radius: 50%;
    z-index: 0;
  }

  &:hover {
    transform: scale(1.1);
  }

  img {
    width: 15px;
    height: 15px;
    position: relative;
    z-index: 1;
  }
}

@media (max-width: 1260px) {
  .button {
    transform: scale(0.8);
    transform-origin: left center;

     &:hover {
      transform: scale(0.8 * 1.1);
    }
  }
}
</style>