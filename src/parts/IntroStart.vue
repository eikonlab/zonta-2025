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
          <div id="layout-title">
            <div id="layout-title-text">
              <p>Une expérience <em>interactive</em> par eikonlab</p>
              <p id="text-discover">Découvrez tous vos <em>messages d'amour</em></p>
            </div>
            <h1>Sapin porte-paroles</h1>
            <p id="text-discover-mobile">Découvrez tous vos <em>messages d'amour</em></p>
          </div>
        </div>
      </div>

      <div id="button-start">
        <ButtonStart @start="$emit('start')"></ButtonStart>
      </div>

      <div class="row">
        <div class="col-12 layout-end-text-col">
          <div id="layout-end-text">
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

.layout-end-text-col {
  position: relative;
  margin-bottom: 20px;
}

#intro-start-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
}

/* Titre et sous titres */
#layout-title {
  display: inline-block;
  padding-top: 100px;
}

#layout-title-text {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

#text-discover-mobile {
  display: none;
}

/* Texte bas */
#layout-end-text {
  text-align: right;
}

#layout-end-text p {
  margin: 0;
}

/* Position du bouton */
#button-start {
  height: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Responsive */
@media (max-width: 992px) {
  #layout-title {
    padding-top: 50px;
  }

  .screen {
    height: 100vh;
  }
}

@media (max-width: 768px) {
  #layout-title {
    padding-top: 40px;
  }

  #layout-title-text {
    display: flex;
    flex-direction: column;
  }

  #text-discover-mobile {
    display: block;
  }

  #text-discover {
    display: none;
  }
}

@media (max-width: 576px) {
  #layout-title {
    padding-top: 10px;
  }

  #layout-end-text {
    text-align: left;
    line-clamp: 3;
  }
}

@media (min-width: 768px) and (max-width: 1200px) {
  #button-start {
    height: 30%;
  }
}
</style>
