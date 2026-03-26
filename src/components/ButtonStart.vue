<script setup>
// ACCUEIL BLOQUÉ
const emit = defineEmits(['start'])

function startExperience() {
  const main = document.querySelector('main')

  emit('start') // 🔥 envoie vers IntroStart

  main.scrollIntoView({
    behavior: 'smooth',
  })
}
</script>

<template>
  <div>
    <a href="#intro-words" class="button-wrapper" @click.prevent="startExperience">
      <div class="button-extern"></div>
      <div class="button-intern">
        <p>
          <strong>Débuter <br />l'expérience</strong>
        </p>
      </div>
    </a>
  </div>
</template>

<style scoped>
.button-wrapper {
  display: inline-block;
  position: relative;
  width: 172px;
  height: 172px;
}

.button-intern p {
  text-align: center;
  color: var(--color-white);
}

/* Cercles */
.button-extern,
.button-intern {
  border-radius: 50%;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);

  display: flex;
  justify-content: center;
  align-items: center;
  transition: all 0.5s ease;
}

/* Img fond */
.button-wrapper::before {
  content: '';
  position: absolute;
  inset: 0;

  background-image: url('../../img-button-start.svg');
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;

  transform: scale(2.5);

  clip-path: circle(0% at 50% 50%);
  opacity: 0;

  transition:
    clip-path 0.8s ease,
    opacity 0.6s ease;
}

.button-wrapper:hover::before {
  clip-path: circle(120% at 50% 50%);
  opacity: 1;
}

/* Grand cercle de base */
.button-extern {
  border: 1.4px solid var(--color-white);
  width: 172px;
  height: 172px;

  z-index: 1;
}

.button-wrapper:hover .button-extern {
  width: 150px;
  height: 150px;

  z-index: 2;
}

/* Petit cercle de base */
.button-intern {
  background-color: #ffb27b;
  width: 106px;
  height: 106px;

  z-index: 2;
}

.button-wrapper:hover .button-intern {
  width: 172px;
  height: 172px;

  z-index: 1;
}
</style>
