<script setup>
import ButtonStart from './../components/ButtonStart.vue'

// ACCUEIL BLOQUÉ
defineEmits(['start'])
</script>

<template>
  <div class="screen" id="intro-start">
    <div id="intro-start-container">
      <div class="row">
        <div class="col-12">
          <div id="intro-start-layout-title">
            <div id="intro-start-layout-title-text">
              <p>Une expérience <em>interactive</em> par eikonlab</p>
              <p id="intro-start-text-discover">Découvrez tous vos <em>messages d'amour</em></p>
            </div>
            <h1>Sapin porte-paroles</h1>
            <p id="intro-start-text-discover-mobile">
              Découvrez tous vos <em>messages d'amour</em>
            </p>
          </div>
        </div>
      </div>

      <div id="intro-start-button-start">
        <ButtonStart @start="$emit('start')"></ButtonStart>
      </div>

      <div class="row">
        <div class="col-12 intro-start-layout-end-text-col">
          <div id="intro-start-layout-end-text">
            <p>
              Une initiative de l'association <em>Victime pas seule</em> relayée par le club service
              <em>Zonta</em>
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.screen {
  position: relative;
}

#intro-start-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
}

/* Titre et sous titres */
#intro-start-layout-title {
  display: inline-block;
  padding-top: 100px;
}

#intro-start-layout-title-text {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

#intro-start-text-discover-mobile {
  display: none;
}

/* Texte bas */
.intro-start-layout-end-text-col {
  position: relative;
  margin-bottom: 20px;
}

#intro-start-layout-end-text {
  text-align: right;
}

#intro-start-layout-end-text p {
  margin: 0;
}

/* Position du bouton */
#intro-start-button-start {
  height: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Responsive */
@media (max-width: 992px) {
  .screen {
    height: 100vh;
  }

  #intro-start-layout-title {
    padding-top: 50px;
  }
}

@media (max-width: 768px) {
  #intro-start-layout-title {
    padding-top: 40px;
  }

  #intro-start-layout-title-text {
    display: flex;
    flex-direction: column;
  }

  #intro-start-text-discover-mobile {
    display: block;
  }

  #intro-start-text-discover {
    display: none;
  }
}

@media (max-width: 576px) {
  #intro-start-layout-title {
    padding-top: 10px;
  }

  #intro-start-layout-end-text {
    text-align: left;
    line-clamp: 3;
  }
}

@media (min-width: 768px) and (max-width: 1200px) {
  #intro-start-button-start {
    height: 30%;
  }
}
</style>
