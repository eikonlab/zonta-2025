<script setup>
import StatsStatistics from './../parts/StatsStatistics.vue'
import StatsHighlightedMessage from './../parts/StatsHighlightedMessage.vue'
import StatsRecurringMessages from './../parts/StatsRecurringMessages.vue'
import StatsAllMessages from './../parts/StatsAllMessages.vue'
import Timeline from './../components/Timeline.vue'

// TEST FRISE
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'
import { onMounted, nextTick } from 'vue'

gsap.registerPlugin(ScrollTrigger)

onMounted(async () => {
  await nextTick()

  const section = document.querySelector('.section-timeline')
  const timeline = document.querySelector('.timeline-container')

  if (!section || !timeline) return

  gsap.to(timeline, {
    y: section.offsetHeight - timeline.offsetHeight,
    ease: 'none',
    scrollTrigger: {
      trigger: section,
      start: 'top top',
      end: 'bottom bottom',
      scrub: true,
      markers: true, // 🔥 debug
    },
  })
})
</script>

<template>
  <div id="burger-recapitulatif" class="burger-blue timeline-parent-position">
    <div id="section-timeline">
      <div id="timeline-container">
        <Timeline></Timeline>
      </div>
    </div>

    <div class="container">
      <StatsStatistics></StatsStatistics>
    </div>

    <div class="container">
      <StatsHighlightedMessage></StatsHighlightedMessage>
    </div>

    <div class="container">
      <StatsRecurringMessages></StatsRecurringMessages>
    </div>

    <div class="container">
      <StatsAllMessages></StatsAllMessages>
    </div>
  </div>
</template>

<style scoped>
/* Position timeline */
#section-timeline {
  position: relative;
}

#timeline-container {
  position: absolute;
  top: 0;
  right: 0;
}
</style>
