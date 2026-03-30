<script setup>
// import { onMounted, nextTick } from 'vue'
// import gsap from 'gsap'
// import ScrollTrigger from 'gsap/ScrollTrigger'

// gsap.registerPlugin(ScrollTrigger)

// onMounted(async () => {
//   await nextTick()

//   const words = gsap.utils.toArray('#layout-all-words p')

//   // état initial → invisible
//   gsap.set(words, {
//     opacity: 0,
//     x: -40,
//   })

//   // timeline liée à la section
//   gsap
//     .timeline({
//       scrollTrigger: {
//         trigger: '#intro-words',
//         start: 'top 100%', // quand on ARRIVE sur la page 2
//         end: 'middle 20%', // quand on QUITTE la page 2
//         scrub: true, // lie au scroll → entrée + sortie auto
//       },
//     })
//     .to(words, {
//       opacity: 1,
//       x: 0,
//       stagger: 0.2,
//       duration: 1,
//       ease: 'power2.out',
//     })
// })
</script>

<template>
  <div class="screen" id="intro-words">
    <div id="layout-all-words">
      <div class="row">
        <div class="col-10 col-lg-12 offset-2 offset-lg-0">
          <div id="layout-courage">
            <p id="word-courage">Courage</p>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-11 offset-1">
          <p id="word-espoir">Espoir</p>
        </div>
      </div>
      <div class="row">
        <div class="col-7 offset-5">
          <p id="word-soutien">Soutien</p>
        </div>
      </div>
      <div class="row">
        <div class="col-5 offset-6 offset-sm-7">
          <p id="word-respect">Respect</p>
        </div>
      </div>
      <div class="row">
        <div class="col-10 offset-2">
          <p id="word-solidarite">Solidarité</p>
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

/* Texte */
p {
  font-family: arima, sans-serif;
  font-size: 68px;
  font-weight: 600;

  background-color: var(--color-light-orange);
  display: inline-block;
  padding: 30px;
  border-radius: 100px;
}

/* Mise en page centrée des mots */
#layout-all-words {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

#layout-all-words .row {
  margin: 0;
}

/* Mise en page mot Courage */
#layout-courage {
  display: flex;
  justify-content: flex-end;
}

/* Placement précis des mots */
#word-espoir {
  margin-top: -50px;
}

#word-soutien {
  margin-top: 20px;
}

#word-respect {
  margin-top: 60px;
}

#word-solidarite {
  margin-top: 30px;
}

/* Responsive */
@media (max-width: 992px) {
  #layout-courage {
    display: flex;
    justify-content: flex-start;
  }

  #word-espoir {
    margin-top: 60px;
  }

  #word-soutien {
    margin-top: 70px;
  }

  #word-respect {
    margin-top: 90px;
  }

  #word-solidarite {
    margin-top: 20px;
  }
}

@media (max-width: 992px) {
  p {
    font-size: 40px;
    padding: 24px;
  }

  #word-espoir {
    margin-top: 45px;
  }

  #word-soutien {
    margin-top: 55px;
  }

  #word-respect {
    margin-top: 75px;
  }

  #word-solidarite {
    margin-top: 10px;
  }
}

@media (max-width: 768px) {
  p {
    font-size: 36px;
    padding: 20px;
  }
}
</style>
