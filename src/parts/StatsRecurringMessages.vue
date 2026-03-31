<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const section = ref(null)
let ctx

onMounted(() => {
  ctx = gsap.context(() => {
    const together = section.value.querySelector('#layout-sentence-top')
    const violence = section.value.querySelector('#sentence-violence')
    const believe = section.value.querySelector('#sentence-believe')
    const report = section.value.querySelector('#sentence-report')
    const title = section.value.querySelector('#layout-title')

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
          <div id="layout-title">
            <h3>Messages les plus récurrents</h3>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-12">
          <div id="layout-sentence-top">
            <div>
              <p class="small-text">Tu n'es</p>
              <p class="big-text">pas seule</p>
            </div>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-md-7 col-lg-6 offset-md-2 offset-lg-3 offset-xl-4">
          <div id="layout-sentences">
            <div id="sentence-violence">
              <p class="small-text">La</p>
              <p class="big-text">violence</p>
              <p class="small-text specific-position-violence" id="specific-margin-violence-bottom">
                n'est
              </p>
              <p class="big-text specific-position-violence">jamais acceptable</p>
            </div>
            <div id="sentence-believe">
              <p class="small-text">Je te</p>
              <p class="big-text">crois</p>
            </div>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-12">
          <div id="sentence-report">
            <p class="small-text" id="specific-position-dont">N'aie</p>
            <p class="big-text" id="specific-position-scared">pas peur</p>
            <p class="small-text" id="specific-margin-report-top-bottom">de</p>
            <p class="big-text">dénoncer</p>
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

#layout-title {
  display: flex;
  justify-content: center;

  margin-bottom: 30px;
  margin-left: 40px;
}

/* Fonts */
.small-text {
  font-family: arima, sans-serif;
  font-size: 20px;
  font-weight: 300;
  line-height: 20px;
  margin: 0;
}

.big-text {
  font-family: arima, sans-serif;
  font-size: 38px;
  font-style: normal;
  font-weight: 600;
  line-height: 30px;
  margin: 0;
}

/* Mise en page */
#layout-sentence-top {
  display: flex;
  justify-content: center;
  margin-bottom: 80px;
}

#layout-sentences {
  display: flex;
  justify-content: space-between;
}

/* Postion horizontal des mots */
#specific-margin-report-top-bottom {
  margin-top: 7px;
  padding-left: 90px;
}

#specific-margin-violence-bottom {
  margin: 6px 0;
}

#layout-sentence-top .small-text {
  padding-left: 20px;
}

#specific-position-scared {
  padding-left: 80px;
}

#specific-position-dont {
  padding-left: 60px;
}

.specific-position-violence {
  padding-left: 80px;
}

#sentence-believe .big-text {
  padding-left: 20px;
}

/* Responsive */
@media (min-width: 992px) {
  .screen {
    padding-left: 60px;
  }
}

@media (max-width: 992px) {
  #sentence-violence {
    margin-bottom: 20px;
  }

  #layout-sentence-top {
    margin-bottom: 60px;
  }

  #layout-title {
    justify-content: flex-end;
  }

  h3 {
    text-align: end;
  }
}

@media (max-width: 830px) {
  #layout-sentences {
    flex-direction: column-reverse;
  }

  #sentence-violence {
    margin-bottom: 60px;
  }

  #layout-sentence-top {
    margin-bottom: 40px;
  }

  #sentence-believe {
    align-self: flex-end;
  }

  #sentence-report {
    margin-left: 30px;
  }
}

@media (max-width: 768px) {
  h3 {
    max-width: 200px;
  }

  .small-text {
    font-size: 16px;
    line-height: 16px;
  }

  .big-text {
    font-size: 30px;

    line-height: 24px;
  }
}

@media (max-width: 576px) {
  h3 {
    max-width: 150px;
  }

  #layout-sentence-top {
    margin-right: 40px;
    margin-top: 20px;
    justify-content: flex-end;
  }
}
</style>
