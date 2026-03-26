<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
gsap.registerPlugin(ScrollTrigger)

const heroImg = ref(null)
const heroContainer = ref(null)
let ctx

onMounted(() => {
  const isMobile = window.innerWidth < 600

  const values = isMobile
    ? {
        startX: '0',
        midX: '0',
        endX: '0',
      }
    : {
        startX: '0',
        midX: '-20%',
        endX: '0',
      }
  ctx = gsap.context(() => {
    gsap.set(heroImg.value, {
      x: values.startX,
      y: values.startY,
    })
  })
})

onUnmounted(() => ctx.revert())
</script>

<template>
  <div class="bg-container">
    <img class="bg-img" src="/bg-p1.svg" alt="" />
    <img class="bg-img-2" src="/bg-p2.svg" alt="" />
    <img class="bg-img-3" src="/bg-p3.svg" alt="" />
  </div>
</template>

<style scoped>
.bg-container {
  position: sticky;
  overflow: hidden;
  inset: 0;
  z-index: 2;
  height: 100vh;
  display: flex;
  flex-flow: row nowrap;
  align-items: center;
  pointer-events: none;
}

.bg-img,
.bg-img-2,
.bg-img-3 {
  position: absolute;
  left: 50%;
  min-width: 100vw;
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

@media (max-aspect-ratio: 19/9) {
  .bg-img,
  .bg-img-2,
  .bg-img-3 {
    height: 100vh;
    min-width: none;
  }
}

/* @media (min-width: 600px) {
  img {
    scale: 500%;
  }
}

@media (min-width: 1400px) {
  img {
    width: 80vw;
  }
} */
</style>
