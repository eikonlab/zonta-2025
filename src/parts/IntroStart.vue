<script setup>
import ButtonStart from './../components/ButtonStart.vue'
</script>

<template>
  <div class="screen">
    <div class="row">
      <div class="col-12">
        <div class="layout-title">
          <div class="layout-title-text">
            <p>Une expérience <em>interactive</em> par eikonlab</p>
            <p>Découvrez tous vos <em>messages d'amour</em></p>
          </div>
          <h1>Sapin porte-paroles</h1>
        </div>
      </div>
    </div>

    <ButtonStart class="button-start"></ButtonStart>

    <div class="row">
      <div class="col-12">
        <div class="layout-end-text">
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

.layout-title {
  display: inline-block;
}

.layout-title-text {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

@media (max-width: 768px) {
  .layout-title-text {
    display: flex;
    flex-direction: column;
  }
}

.layout-end-text {
  height: 12vh;
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
}

/* Button position */
.button-start {
  height: 50vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
