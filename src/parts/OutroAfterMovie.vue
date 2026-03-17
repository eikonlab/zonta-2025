<script setup></script>

<template>
  <div class="screen">
    <div class="row">
      <div class="col-12 col-lg-2" id="layout-margin">
        <h3>Retour en image</h3>
      </div>
      <div class="col-12 col-lg-8">
        <div class="video"></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Font */
h3 {
  color: var(--color-white);
  text-align: end;
}

/* Style vidéo */
.video {
  width: 100%;
  aspect-ratio: 5 / 4;
  background-color: var(--color-white);
}

/* Mise en page */
#layout-margin {
  padding: 8px 0;
}

@media (max-width: 992px) {
  .screen {
    height: 100vh;
  }

  h3 {
    text-align: start;
    line-height: 25px;
  }

  #layout-margin {
    padding: 12px 12px 0;
  }
}
</style>
