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
    <img ref="heroImg" class="bg-img" src="/background-test-nocrop.svg" alt="" />
  </div>
</template>

<style scoped>
.bg-container {
  position: fixed;
  overflow: hidden;
  top: 0;
  left: 0;
  z-index: 2;
  height: 100vh;
  width: 100%;
  display: flex;
  flex-flow: row nowrap;
  align-items: center;
  pointer-events: none;
}

.bg-img {
  width: auto;
  height: auto;
  pointer-events: none;
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
