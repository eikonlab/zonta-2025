<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
gsap.registerPlugin(ScrollTrigger)

const heroImg = ref(null)
const heroContainer = ref(null)
let ctx // ← manquant

onMounted(() => {
  const isMobile = window.innerWidth < 576

  const values = isMobile
    ? {
        startX: '140%',
        startY: '-15%',
        midX: '-65%',
        midY: '-55%',
        endX: '-5%',
        endY: '-180%',
      }
    : {
        startX: '175%',
        startY: '-15%',
        midX: '-65%',
        midY: '-55%',
        endX: '-5%',
        endY: '-180%',
      }
  ctx = gsap.context(() => {
    gsap.set(heroImg.value, {
      x: values.startX,
      y: values.startY,
    })

    const tl = gsap.timeline({
      scrollTrigger: {
        trigger: heroContainer.value,
        start: 'top top',
        end: 'bottom-=33% top',
        scrub: 2,
        // markers: true,
        // invalidateOnRefresh: true,
      },
    })

    // 1ère moitié du scroll → point A
    tl.to(heroImg.value, {
      x: values.midX,
      y: values.midY,
      ease: 'power3.inOut',
    })

    // 2ème moitié du scroll → point B
    tl.to(heroImg.value, {
      x: values.endX,
      y: values.endY,
      ease: 'power3.inOut',
    })
  })
})

onUnmounted(() => ctx.revert())
</script>

<template>
  <div class="absolute-container">
    <div ref="heroContainer" class="relative-container">
      <div class="heroContainer">
        <img ref="heroImg" class="heroImg" src="/sapin.svg" alt="" />
      </div>
    </div>
  </div>
</template>

<style scoped>
:global(html),
:global(body) {
  padding: 0;
  margin: 0;
}

.absolute-container {
  position: absolute;
  inset: 0;
  z-index: -1;
  height: 300vh;
  overflow: clip;
}

.relative-container {
  position: relative;
  height: 300vh;
  /* overflow: hidden; */
}

.heroContainer {
  position: sticky;
  width: 100%;
  height: 100svh;
  inset: 0;
}

img {
  width: 1200px;
  scale: 450%;
  position: absolute;
  pointer-events: none;
  top: 0;
  left: 0;
  opacity: 0.5;
  /* transition: all 3s ease; */
}

@media (min-width: 600px) {
  img {
    scale: 500%;
    opacity: 1;
  }
}

@media (min-width: 1400px) {
  img {
    width: 80vw;
  }
}
</style>
