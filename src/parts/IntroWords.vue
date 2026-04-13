<script setup>
import gsap from 'gsap'
import { onMounted, ref, watch } from 'vue'

const wordsList = ref(null)
defineEmits(['nextSection'])

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
      gsap.to(wordsList.value, {
        opacity: 1,
        duration: 1,
        ease: 'power2.out',
        stagger: 0.3,
      })
    } else {
      gsap.set(wordsList.value, {
        opacity: 0,
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
    <button @click="$emit('nextSection')" id="next-section-1">
      <span class="icon">
        <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M4.29289 8.29289C4.68342 7.90237 5.31658 7.90237 5.70711 8.29289L12 14.5858L18.2929 8.29289C18.6834 7.90237 19.3166 7.90237 19.7071 8.29289C20.0976 8.68342 20.0976 9.31658 19.7071 9.70711L12.7071 16.7071C12.3166 17.0976 11.6834 17.0976 11.2929 16.7071L4.29289 9.70711C3.90237 9.31658 3.90237 8.68342 4.29289 8.29289Z"
            fill="currentColor"
          />
        </svg>
      </span>
    </button>
  </div>
</template>

<style scoped>
.screen {
  display: flex;
  align-items: center;
  position: relative;
}

/* Texte */
p {
  font-family: arima, sans-serif;
  font-size: 68px;
  font-weight: 600;

  display: inline-block;
  padding: 30px;

  background-color: var(--color-light-orange);
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

#next-section-1 {
  position: absolute;
  bottom: 5%;
  left: 50%;
  transform: translateX(-50%);
  background: none;
  color: white;
  border: none;
  z-index: 10;
}

#next-section-1 .icon {
  border: 1px solid white;
  width: 40px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  animation: pulse 3s infinite;
}

#next-section-1 .icon svg {
  width: 24px;
}

@keyframes pulse {
  0% {
    transform: scale(1);
  }

  50% {
    transform: scale(1.3);
  }

  100% {
    transform: scale(1);
  }
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

@media (max-width: 576px) {
  #next-section-1 {
    left: 85%;
    transform: translateX(0);
  }
}
</style>
