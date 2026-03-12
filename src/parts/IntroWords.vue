<script setup></script>

<template>
  <div class="screen">
    <div class="row">
      <div class="col-11 offset-1">
        <div class="layout-content">
          <p class="word-espoir">Espoir</p>
          <p>Courage</p>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col-7 offset-5">
        <p class="word-soutien">Soutien</p>
      </div>
    </div>
    <div class="row">
      <div class="col-5 offset-7">
        <p class="word-respect">Respect</p>
      </div>
    </div>
    <div class="row">
      <div class="col-10 offset-2">
        <p>Solidarité</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.screen {
  height: 100vh;
}

p {
  font-family: arima, sans-serif;
  font-size: 68px;
  font-weight: 600;
}

/* Mise en page mots Espoir et Courage */
.layout-content {
  display: flex;
  justify-content: space-between;
}

/* Placement mots */
.word-espoir {
  margin-top: 15px;
}

.word-soutien {
  margin-top: 60px;
}

.word-respect {
  margin-top: 80px;
}

@media (max-width: 576px) {
  p {
    font-size: 36px;
  }
}
</style>
