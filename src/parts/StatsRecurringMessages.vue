<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const section = ref(null)
let ctx

onMounted(() => {
  ctx = gsap.context(() => {
    const together = section.value.querySelector('#stats-recurring-layout-sentence-top')
    const violence = section.value.querySelector('#stats-recurring-sentence-violence')
    const believe = section.value.querySelector('#stats-recurring-sentence-believe')
    const report = section.value.querySelector('#stats-recurring-sentence-report')
    const title = section.value.querySelector('#stats-recurring-layout-title')

    const tl = gsap.timeline({
      scrollTrigger: {
        trigger: section.value,
        start: 'center 80%',
        toggleActions: 'play reverse play reverse',
      },
    })

    tl.from(title, {
      opacity: 0,
      y: 40,
      duration: 0.6,
      ease: 'power2.out',
    })

    tl.from(together, {
      opacity: 0,
      y: 40,
      duration: 0.6,
      ease: 'power2.out',
    })

    tl.from(violence, {
      opacity: 0,
      y: 40,
      duration: 0.6,
      ease: 'power2.out',
    })

    tl.from(believe, {
      opacity: 0,
      y: 40,
      duration: 0.6,
      ease: 'power2.out',
    })

    tl.from(report, {
      opacity: 0,
      y: 40,
      duration: 0.6,
      ease: 'power2.out',
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
          <div id="stats-recurring-layout-title">
            <h2>Messages les plus récurrents</h2>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-12">
          <div id="stats-recurring-layout-sentence-top">
            <div>
              <p class="stats-recurring-small-text">Tu n'es</p>
              <p class="stats-recurring-big-text">pas seule</p>
            </div>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-md-7 col-lg-7 offset-md-2 offset-lg-3 offset-xl-4">
          <div id="stats-recurring-layout-sentences">
            <div id="stats-recurring-sentence-violence">
              <p class="stats-recurring-small-text">La</p>
              <p class="stats-recurring-big-text">violence</p>
              <p
                class="stats-recurring-small-text stats-recurring-specific-position-violence"
                id="stats-recurring-specific-margin-violence-bottom"
              >
                n'est
              </p>
              <p class="stats-recurring-big-text stats-recurring-specific-position-violence">
                jamais acceptable
              </p>
            </div>
            <div id="stats-recurring-sentence-believe">
              <p class="stats-recurring-small-text">Je te</p>
              <p class="stats-recurring-big-text">crois</p>
            </div>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-12">
          <div id="stats-recurring-sentence-report">
            <p class="stats-recurring-small-text" id="stats-recurring-specific-position-dont">
              N'aie
            </p>
            <p class="stats-recurring-big-text" id="stats-recurring-specific-position-scared">
              pas peur
            </p>
            <p
              class="stats-recurring-small-text"
              id="stats-recurring-specific-margin-report-top-bottom"
            >
              de
            </p>
            <p class="stats-recurring-big-text">dénoncer</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.screen {
  padding-top: 6%;
}

#stats-recurring-layout-title {
  display: flex;
  justify-content: center;

  margin-bottom: 30px;
  margin-left: 40px;
}

/* Fonts */
.stats-recurring-small-text {
  font-family: arima, sans-serif;
  font-size: 20px;
  font-weight: 300;
  line-height: 20px;
  margin: 0;
}

.stats-recurring-big-text {
  font-family: arima, sans-serif;
  font-size: 38px;
  font-style: normal;
  font-weight: 600;
  line-height: 30px;
  margin: 0;
}

/* Mise en page */
#stats-recurring-layout-sentence-top {
  display: flex;
  justify-content: center;
  margin-bottom: 80px;
}

#stats-recurring-layout-sentences {
  display: flex;
  justify-content: space-between;
}

/* Postion horizontal des mots */
#stats-recurring-specific-margin-report-top-bottom {
  margin-top: 7px;
  padding-left: 90px;
}

#stats-recurring-specific-margin-violence-bottom {
  margin: 6px 0;
}

#stats-recurring-layout-sentence-top .small-text {
  padding-left: 20px;
}

#stats-recurring-specific-position-scared {
  padding-left: 80px;
}

#stats-recurring-specific-position-dont {
  padding-left: 60px;
}

.stats-recurring-specific-position-violence {
  padding-left: 80px;
}

#stats-recurring-sentence-believe .big-text {
  padding-left: 20px;
}

/* Responsive */
@media (min-width: 992px) {
  .screen {
    padding-left: 60px;
  }
}

@media (max-width: 992px) {
  #stats-recurring-sentence-violence {
    margin-bottom: 20px;
  }

  #stats-recurring-layout-sentence-top {
    margin-bottom: 60px;
  }

  #stats-recurring-layout-title {
    justify-content: flex-end;
  }

  h2 {
    text-align: end;
  }
}

@media (max-width: 830px) {
  #stats-recurring-layout-sentences {
    flex-direction: column-reverse;
  }

  #stats-recurring-sentence-violence {
    margin-bottom: 60px;
  }

  #stats-recurring-layout-sentence-top {
    margin-bottom: 40px;
  }

  #stats-recurring-sentence-believe {
    align-self: flex-end;
  }

  #stats-recurring-sentence-report {
    margin-left: 30px;
  }
}

@media (max-width: 768px) {
  h2 {
    max-width: 200px;
  }

  .stats-recurring-small-text {
    font-size: 16px;
    line-height: 16px;
  }

  .stats-recurring-big-text {
    font-size: 30px;

    line-height: 24px;
  }
}

@media (max-width: 576px) {
  h2 {
    max-width: 150px;
  }

  #stats-recurring-layout-sentence-top {
    margin-right: 40px;
    margin-top: 20px;
    justify-content: flex-end;
  }
}
</style>
