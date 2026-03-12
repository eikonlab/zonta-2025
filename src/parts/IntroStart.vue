<script setup>
import ButtonStart from './../components/ButtonStart.vue'
</script>

<template>
  <div class="screen">
    <div class="row">
      <div class="col-12">
        <div id="layout-title">
          <div id="layout-title-text">
            <p>Une expérience <em>interactive</em> par eikonlab</p>
            <p>Découvrez tous vos <em>messages d'amour</em></p>
          </div>
          <h1>Sapin porte-paroles</h1>
        </div>
      </div>
    </div>

    <ButtonStart id="button-start"></ButtonStart>

    <div class="row">
      <div class="col-12">
        <div id="layout-end-text">
          <p>
            Une initiative de l'association <em>Victime pas seule</em> relayée par le club service
            <em>Zonta</em>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.screen {
  height: 100vh;
}

/* Titre et sous titres */
#layout-title {
  display: inline-block;
}

#layout-title-text {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

/* Texte bas */
#layout-end-text {
  height: 12vh;
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
}

/* Position du bouton */
#button-start {
  height: 50vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Responsive */
@media (max-width: 768px) {
  #layout-title-text {
    display: flex;
    flex-direction: column;
  }
}
</style>
