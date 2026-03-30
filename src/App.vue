<script setup>
import PartOutro from './sections/SectionOutro.vue'
import PartIntro from './sections/SectionIntro.vue'
import PartStats from './sections/SectionStats.vue'
import BurgerMenu from './components/BurgerMenu.vue'

import Timeline from './components/Timeline.vue'
import TimelineMobile from './components/TimelineMobile.vue'

import { onMounted, onBeforeUnmount } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

// Frise
gsap.registerPlugin(ScrollTrigger)

onMounted(() => {
  const mm = gsap.matchMedia()

  // Frise desktop
  mm.add('(min-width: 993px)', () => {
    const timeline = document.querySelector('#timeline-content')

    if (!timeline) return

    const getMoveY = () => {
      const timelineHeight = timeline.scrollHeight
      const viewportHeight = window.innerHeight

      return Math.max(timelineHeight - viewportHeight, 0)
    }

    gsap.to(timeline, {
      y: () => -getMoveY(),
      ease: 'none',
      scrollTrigger: {
        trigger: '#main',
        start: 'top top',
        end: '+=300%',
        scrub: true,
        invalidateOnRefresh: true,
        markers: false,
      },
    })
  })

  mm.add('(max-width: 992px)', () => {
    const timeline = document.querySelector('#timeline-content-mobile')
    const section = document.querySelector('#main')

    if (!timeline || !section) return

    const getMoveX = () => {
      return timeline.scrollWidth - window.innerWidth
    }

    const getScroll = () => {
      return section.offsetHeight - window.innerHeight
    }

    if (getMoveX() <= 0) return

    gsap.to(timeline, {
      x: () => -getMoveX(),
      ease: 'none',
      scrollTrigger: {
        trigger: section,
        start: 'top top',
        end: () => `+=${getScroll()}`,
        scrub: true,
        invalidateOnRefresh: true,
      },
    })
  })
})

// Animmation apparition texte
// onMounted(() => {
//   const items = document.querySelectorAll('.timeline-item')

//   function updateItems() {
//     items.forEach((item) => {
//       const rect = item.getBoundingClientRect()
//       const viewportCenter = window.innerHeight / 2

//       const date = item.querySelector('.date')
//       const location = item.querySelector('.location')

//       if (!date || !location) return

//       // 🔥 distance au centre
//       const itemCenter = rect.top + rect.height / 2
//       const distance = Math.abs(viewportCenter - itemCenter)

//       // 🔥 zone active (à ajuster)
//       const threshold = 200

//       if (distance < threshold) {
//         // visible → on montre
//         gsap.to([date, location], {
//           opacity: 1,
//           y: 0,
//           duration: 0.3,
//           overwrite: true,
//         })
//       } else {
//         // hors centre → on cache
//         gsap.to([date, location], {
//           opacity: 0,
//           y: 10,
//           duration: 0.3,
//           overwrite: true,
//         })
//       }
//     })
//   }

//   // 🔥 sync avec GSAP scroll
//   gsap.ticker.add(updateItems)

//   // cleanup (important en Vue)
//   onBeforeUnmount(() => {
//     gsap.ticker.remove(updateItems)
//   })
// })

onMounted(() => {
  const items = document.querySelectorAll('.timeline-item')

  function updateItems() {
    items.forEach((item) => {
      const rect = item.getBoundingClientRect()
      // const viewportCenter = window.innerHeight / 2

      const date = item.querySelector('.date')
      const location = item.querySelector('.location')
      const age = item.querySelector('.age')
      const line = item.querySelector('.big-line')

      if (!date || !location || !age || !line) return

      const itemCenter = rect.top + rect.height / 2

      const start = window.innerHeight * 0.35
      const end = window.innerHeight * 0.65

      const isActive = itemCenter > start && itemCenter < end

      // 🔥 éviter de relancer l’anim en boucle
      if (item._active === isActive) return
      item._active = isActive

      if (isActive) {
        // 🟢 ÉTAT ACTIF
        gsap.to([date, location], {
          opacity: 1,
          y: 0,
          duration: 0.3,
          ease: 'power2.out',
        })

        gsap.to(age, {
          y: 0,
          duration: 0.3,
          ease: 'power2.out',
        })

        gsap.to(line, {
          scaleX: 1,
          x: 0,
          duration: 0.3,
          ease: 'power2.out',
        })
      } else {
        // 🔴 ÉTAT COMPACT
        gsap.to([date, location], {
          opacity: 0,
          y: 10,
          duration: 0.3,
          ease: 'power2.in',
        })

        gsap.to(age, {
          y: -10,
          duration: 0.3,
          ease: 'power2.in',
        })

        gsap.to(line, {
          scaleX: 0.3,
          x: 130, // 🔥 ton besoin ici
          duration: 0.3,
          ease: 'power2.in',
        })
      }
    })
  }

  // 🔥 sync avec GSAP scroll
  gsap.ticker.add(updateItems)

  // cleanup (important en Vue)
  onBeforeUnmount(() => {
    gsap.ticker.remove(updateItems)
  })
})
</script>

<template>
  <div id="website">
    <BurgerMenu></BurgerMenu>

    <header>
      <PartIntro></PartIntro>
    </header>

    <main id="main">
      <div id="timeline-blur-wrapper">
        <div id="timeline-blur"></div>
      </div>

      <div id="timeline-container-mobile">
        <div id="timeline-content-mobile">
          <TimelineMobile></TimelineMobile>
        </div>
      </div>

      <div id="timeline-container-desktop">
        <div id="timeline-content">
          <Timeline></Timeline>
        </div>
      </div>

      <div id="section-content">
        <PartStats></PartStats>
      </div>
    </main>

    <footer>
      <PartOutro></PartOutro>
    </footer>
  </div>
</template>

<style scoped>
/* #website {
  overflow: hidden;
} */

/* Contenu entier et position frise */
#main {
  position: relative;
  width: 100%;

  display: flex;
  flex-direction: row-reverse;
}

/* Timeline fond flou  */
#timeline-blur-wrapper {
  position: absolute;
  height: 100%;
}

#timeline-blur {
  position: sticky;
  top: 0;
  right: 0;

  width: 230px;
  height: 100vh;

  background-color: rgba(255, 255, 255, 0.25);
  backdrop-filter: blur(25px);
  -webkit-backdrop-filter: blur(25px);

  z-index: 5;
}

/* Frise mobile */
#timeline-container-mobile {
  position: sticky;
  bottom: 0;
  left: 0;
  z-index: 20;
  pointer-events: none;

  width: 100%;
  height: auto;

  display: none;
  opacity: 0;
  overflow: hidden;
}

#timeline-content-mobile {
  width: max-content;
}

/* Frise desktop */
#timeline-container-desktop {
  width: 230px;
  height: 100vh;
  position: sticky;
  top: 0;
  z-index: 10;
  pointer-events: none;
  overflow: hidden;
  flex-shrink: 0;

  background: none;

  -webkit-mask-image: linear-gradient(to bottom, transparent 0%, black 15%, black 100%);
  mask-image: linear-gradient(to bottom, transparent 0%, black 15%, black 100%);
}

#timeline-content {
  width: 100%;
  height: auto;
}

#main #section-content {
  flex: 1;
  min-width: 0;
}

/* Responsive */
@media (max-width: 992px) {
  #main {
    flex-direction: column-reverse;
  }

  #timeline-container-mobile {
    display: block;
    opacity: 1;
  }

  #timeline-container-desktop {
    display: none;
    opacity: 0;
  }

  #timeline-blur-wrapper {
    display: none;
    opacity: 0;
  }
}
</style>
