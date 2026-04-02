<script setup>
import gsap from 'gsap'
import { onMounted, ref, watch } from 'vue'

const wordsList = ref(null)

const props = defineProps({
  state: Number,
})

onMounted(() => {
  wordsList.value = document.querySelectorAll('#intro-words p')
  gsap.set(wordsList.value, {
    opacity: 0,
  })
})

watch(
  () => props.state,
  (newValue) => {
    if (newValue === 2) {
      console.log(props.state)
      gsap.to(wordsList.value, {
        opacity: 1,
        duration: 1,
        ease: 'power2.out',
        stagger: 0.3,
      })
    }
  },
)
</script>

<template>
  <div class="screen" id="intro-words">
    <div id="intro-words-layout-all-words">
      <div class="row">
        <div class="col-10 col-lg-12 offset-2 offset-lg-0">
          <div id="intro-words-layout-courage">
            <p id="intro-words-word-courage">Courage</p>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-11 offset-1">
          <p id="intro-words-word-espoir">Espoir</p>
        </div>
      </div>
      <div class="row">
        <div class="col-7 offset-5">
          <p id="intro-words-word-soutien">Soutien</p>
        </div>
      </div>
      <div class="row">
        <div class="col-5 offset-6 offset-sm-7">
          <p id="intro-words-word-respect">Respect</p>
        </div>
      </div>
      <div class="row">
        <div class="col-10 offset-2">
          <p id="intro-words-word-solidarite">Solidarité</p>
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
#intro-words-layout-all-words {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  z-index: 1;
}

#intro-words-layout-all-words .row {
  margin: 0;
}

/* Mise en page mot Courage */
#intro-words-layout-courage {
  display: flex;
  justify-content: flex-end;
}

/* Placement précis des mots */
#intro-words-word-courage {
  margin-top: 70px;
}

#intro-words-word-espoir {
  margin-top: -50px;
}

#intro-words-word-soutien {
  margin-top: 20px;
}

#intro-words-word-respect {
  margin-top: 60px;
}

#intro-words-word-solidarite {
  margin-top: 30px;
}

/* Responsive */
@media (max-width: 992px) {
  #intro-words-layout-courage {
    display: flex;
    justify-content: flex-start;
  }

  #intro-words-word-espoir {
    margin-top: 60px;
  }

  #intro-words-word-soutien {
    margin-top: 70px;
  }

  #intro-words-word-respect {
    margin-top: 90px;
  }

  #intro-words-word-solidarite {
    margin-top: 20px;
  }
}

@media (max-width: 992px) {
  p {
    font-size: 40px;
    padding: 24px;
  }

  #intro-words-word-espoir {
    margin-top: 45px;
  }

  #intro-words-word-soutien {
    margin-top: 55px;
  }

  #intro-words-word-respect {
    margin-top: 75px;
  }

  #intro-words-word-solidarite {
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
