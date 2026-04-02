<script setup>
import PartOutro from './sections/SectionOutro.vue'
import PartIntro from './sections/SectionIntro.vue'
import PartStats from './sections/SectionStats.vue'
import BurgerMenu from './components/BurgerMenu.vue'

import Timeline from './components/Timeline.vue'
import TimelineMobile from './components/TimelineMobile.vue'

import { onMounted, ref, provide } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

// Frise
gsap.registerPlugin(ScrollTrigger)

const isIntroDone = ref(false)
const setIntroDDone = (val) => {
  isIntroDone.value = val
}
provide('isIntroDone', isIntroDone)
provide('setIntroDone', setIntroDDone)

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

  // Frise mobile
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

    // Animation apparition texte
    const mobileItems = gsap.utils.toArray('#timeline-mobile-text-layout')

    function updateMobileItems() {
      const viewportCenterX = window.innerWidth / 2
      const activeRange = window.innerWidth * 0.15

      mobileItems.forEach((item) => {
        const rect = item.getBoundingClientRect()
        const itemCenterX = rect.left + rect.width / 2
        const isActive = Math.abs(itemCenterX - viewportCenterX) < activeRange

        if (item._activeMobile === isActive) return
        item._activeMobile = isActive

        if (isActive) {
          gsap.to(item, {
            scale: 1,
            duration: 0.2,
            ease: 'power2.out',
            overwrite: 'auto',
          })
        } else {
          gsap.to(item, {
            scale: 0.9,
            duration: 0.2,
            ease: 'power2.in',
            overwrite: 'auto',
          })
        }
      })
    }

    // Animation frise
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

        onUpdate: updateMobileItems,
      },
    })
  })
})

// Animation apparition texte desktop
onMounted(() => {
  const items = gsap.utils.toArray('.timeline-text-item')

  function updateItems() {
    items.forEach((item) => {
      const rect = item.getBoundingClientRect()
      // const viewportCenter = window.innerHeight / 2

      const date = item.querySelector('.timeline-text-date')
      const location = item.querySelector('.timeline-text-location')
      const age = item.querySelector('.timeline-text-age')
      const line = item.querySelector('.timeline-text-big-line')
      const ageLine = item.querySelector('.timeline-text-age-line')
      const ageWrapper = item.querySelector('.timeline-text-layout-line-age')

      if (!date || !location || !age || !line || !ageLine || !ageWrapper) return

      const itemCenter = rect.top + rect.height / 2

      const start = window.innerHeight * 0.35
      const end = window.innerHeight * 0.65

      const isActive = itemCenter > start && itemCenter < end

      if (item._active === isActive) return
      item._active = isActive

      if (isActive) {
        // État actif
        gsap.to([date, location], {
          opacity: 1,
          y: 0,
          duration: 0.3,
          ease: 'power2.out',
          overwrite: 'auto',
        })

        gsap.to(line, {
          opacity: 1,
          x: 0,
          duration: 0.3,
          ease: 'power2.out',
          overwrite: 'auto',
        })

        gsap.to(age, {
          scale: 1,
          duration: 0.2,
          ease: 'power2.in',
          overwrite: 'auto',
        })

        gsap.to(ageLine, {
          opacity: 0,
          x: 140,
          duration: 0.2,
          ease: 'power2.out',
          overwrite: 'auto',
        })

        gsap.to(ageWrapper, {
          y: 0,
          duration: 0.3,
          ease: 'power2.out',
          overwrite: 'auto',
        })
      } else {
        // État initial
        gsap.to([date, location], {
          opacity: 0,
          y: 10,
          duration: 0.3,
          ease: 'power2.in',
          overwrite: 'auto',
        })

        gsap.to(line, {
          opacity: 0,
          x: 140,
          duration: 0.3,
          ease: 'power2.in',
          overwrite: 'auto',
          pointerEvents: 'none',
        })

        gsap.to(age, {
          scale: 0.9,
          duration: 0.2,
          ease: 'power2.in',
          overwrite: 'auto',
        })

        gsap.to(ageLine, {
          opacity: 1,
          x: 0,
          duration: 0.2,
          overwrite: 'auto',
        })

        gsap.to(ageWrapper, {
          y: -38,
          duration: 0.3,
          ease: 'power2.in',
          overwrite: 'auto',
        })
      }
    })
  }

  ScrollTrigger.create({
    trigger: '#main',
    start: 'top bottom',
    end: 'bottom top',
    onUpdate: updateItems,
  })

  window.addEventListener('resize', () => {
    ScrollTrigger.refresh()
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
