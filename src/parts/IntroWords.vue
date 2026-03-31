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
  z-index: 1;
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
