<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const section = ref(null)
let ctx

onMounted(() => {
  ctx = gsap.context(() => {
    const number = section.value.querySelector('#stats-statistics-layout-number')
    const sentence = section.value.querySelector('#stats-statistics-layout-support-sentence')

    const tl = gsap.timeline({
      scrollTrigger: {
        trigger: section.value,
        start: 'center 80%',
        end: () => `+=${window.innerHeight * 0.6}`,
        toggleActions: 'play reverse play reverse',
      },
    })

    tl.from(number, {
      opacity: 0,
      y: 40,
      duration: 0.6,
      ease: 'power2.out',
    })

    tl.from(sentence, {
      opacity: 0,
      y: 40,
      duration: 0.6,
      ease: 'power2.out',
      delay: 0.2,
    })
  })
})

onBeforeUnmount(() => ctx?.revert())
</script>

<template>
  <div class="screen">
    <div ref="section">
      <div class="row">
        <div class="col-12">
          <div id="stats-statistics-layout-page">
            <div id="stats-statistics-layout-number">
              <p id="stats-statistics-big-text">185</p>
              <p id="stats-statistics-sentence-number-messages">Messages <em>récoltés</em></p>
            </div>
            <div id="stats-statistics-layout-support-sentence">
              <p>
                Tant de messages
                <em
                  >d'amour
                  <img src="/img-icon-words-heart.webp" id="stats-statistics-icon-heart" alt="" loading="lazy"
                /></em>
                et de
                <em
                  >soutien
                  <img src="/img-icon-words-hand.webp" id="stats-statistics-icon-hand" alt="" loading="lazy"
                /></em>
                partagés cette année
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.screen {
  display: flex;
  align-items: center;
}

/* Font */
#stats-statistics-big-text {
  font-family: arima, sans-serif;
  font-size: 250px;
  font-weight: 400;
  line-height: 250px;
  margin: 0;
  height: 250px;
}

/* Mise en page */
#stats-statistics-layout-page {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  padding-top: 10%;
}

#stats-statistics-layout-number {
  display: flex;
  align-items: baseline;
}

/* Icones */
em {
  position: relative;
}

img {
  width: 38px;
  height: auto;
  position: absolute;
  opacity: 0.3;
}

#stats-statistics-icon-heart {
  top: -38px;
  right: -20px;
}

#stats-statistics-icon-hand {
  bottom: -38px;
  right: -20px;
}

@media (max-width: 1253px) {
  #stats-statistics-icon-hand {
    right: -40px;
  }
}

@media (max-width: 1216px) {
  #stats-statistics-icon-heart {
    top: -64px;
    right: -20px;
  }

  #stats-statistics-icon-hand {
    bottom: -68px;
    right: -40px;
  }
}

@media (max-width: 1200px) {
  #stats-statistics-layout-page {
    flex-direction: column;
  }

  #stats-statistics-layout-support-sentence {
    margin-top: 50px;
    text-align: right;
  }

  #stats-statistics-icon-heart {
    top: -38px;
    right: -20px;
  }

  #stats-statistics-icon-hand {
    bottom: -38px;
    right: -20px;
  }
}

@media (min-width: 992px) {
  .screen {
    padding-left: 70px;
  }

  #stats-statistics-sentence-number-messages {
    width: 210px;
  }
}

@media (max-width: 576px) {
  #stats-statistics-big-text {
    font-family: arima, sans-serif;
    font-size: 140px;
    font-weight: 400;
    line-height: 250px;
    margin: 0;
    height: 250px;
  }

  #stats-statistics-icon-hand {
    bottom: -38px;
    right: -20px;
  }
}

@media (max-width: 531px) {
  #stats-statistics-big-text {
    font-family: arima, sans-serif;
    font-size: 140px;
    font-weight: 400;
    line-height: 250px;
    margin: 0;
    height: 250px;
  }

  #stats-statistics-icon-hand {
    bottom: -64px;
    right: -20px;
  }

  #stats-statistics-layout-support-sentence {
    padding-left: 40px;
  }
}

@media (max-width: 500px) {
  #stats-statistics-icon-hand {
    bottom: -64px;
    right: 0;
  }
}

@media (max-width: 422px) {
  #stats-statistics-icon-hand {
    bottom: -68px;
    right: 5px;
  }
}
</style>
