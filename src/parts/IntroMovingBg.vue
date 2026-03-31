<script setup>
import { ref, onMounted, onUnmounted, watch } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
gsap.registerPlugin(ScrollTrigger)

const introContainer = ref(null)
const bgContainerRef = ref(null)
let ctx = ref(null)
const bgImgLast = ref(null)
const bgImgLastOrange = ref(null)
let imageWidth

const props = defineProps({
  state: Number,
})

const animate = (newState, transition) => {
  gsap.to(bgContainerRef.value, {
    x:
      newState === 1
        ? 0
        : newState === 2
          ? -imageWidth
          : newState === 3
            ? -imageWidth * 2
            : -imageWidth * 2,
    duration: transition ? 0.5 : 0,
  })
}

onMounted(() => {
  bgImgLast.value.onload = () => {
    const rect = bgImgLast.value.getBoundingClientRect()
    imageWidth = rect.width
    console.log('imageWidth', imageWidth)
    animate(props.state, false)
  }
  // Si déjà cachée
  if (bgImgLast.value.complete) {
    bgImgLast.value.onload()
  }
})

watch(
  () => props.state,
  (newState) => {
    animate(newState, true)
    if (newState === 4) {
      gsap.to(bgImgLast.value, {
        scale: 1.2,
        duration: 0.5,
      })
      gsap.to(bgImgLastOrange.value, {
        scale: 1.2,
        duration: 0.5,
      })
    }
  },
)

onUnmounted(() => ctx.value.revert())
</script>

<template>
  <div ref="introContainer" id="scroll-zone">
    <div ref="bgContainerRef" class="bg-container">
      <img class="bg-img" src="/bg-p1.svg" alt="" />
      <img class="bg-img-2" src="/bg-p2.svg" alt="" />
      <!-- <div></div> -->
      <img ref="bgImgLast" class="bg-img-3" src="/bg-p3-v2.svg" alt="" />
      <img ref="bgImgLastOrange" class="bg-img-3-orange" src="/bg-p3-v2-orange.svg" alt="" />
    </div>
  </div>
  <div class="mobile-bg-container">
    <img class="mobile-bg" src="/intro-mobile-bg.svg" alt="" />
  </div>
</template>

<style scoped>
#scroll-zone {
  position: absolute;
  inset: 0;
  height: 100%;
  pointer-events: none;
  overflow: clip;
}

.bg-container {
  display: none;
  position: sticky;
  top: 0;
  bottom: 0;
  /* z-index: inherit; */
  height: 100vh;
  display: flex;
  flex-flow: row nowrap;
  align-items: center;
  pointer-events: none;
}

.mobile-bg-container {
  position: absolute;
  top: 0;
  left: 0;
  overflow: clip;
  /* overflow: hidden; */
  /* z-index: 0; */
  width: 100%;
  height: 400vh;
  pointer-events: none;
}

.mobile-bg {
  height: 100%;
  left: 50%;
  transform: translateX(-50%);
  width: auto;
  position: absolute;
}

.bg-img,
.bg-img-2,
.bg-img-3,
.bg-img-3-orange {
  position: absolute;
  left: 50%;
  min-width: 100vw;
  display: none;
}

.bg-img {
  transform: translate(-50%, 0);
}

.bg-img-2 {
  transform: translate(50%, 0);
}

.bg-img-3 {
  transform: translate(150%, 0);
}

.bg-img-3-orange {
  z-index: 2;
  transform: translate(150%, 0);
}

@media (max-aspect-ratio: 19/9) {
  .bg-img,
  .bg-img-2,
  .bg-img-3,
  .bg-img-3-orange {
    height: 100vh;
    min-width: none;
  }
}

@media (min-width: 576px) {
  .mobile-bg-container,
  .mobile-bg {
    display: none;
  }

  .bg-container {
    display: block;
  }

  .bg-img,
  .bg-img-2,
  .bg-img-3,
  .bg-img-3-orange {
    display: block;
  }
}
</style>
