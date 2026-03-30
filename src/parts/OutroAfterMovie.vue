<script setup></script>

<template>
  <div class="screen">
    <div class="row">
      <div class="col-12 col-lg-2" id="layout-margin">
        <h3>Retour en image</h3>
      </div>
      <div class="col-12 col-lg-10">
        <div class="video"></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.screen {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
}

/* Font */
h3 {
  color: var(--color-white);
  text-align: end;
}

.row {
  margin: 0 !important;
  padding: 0 !important;
  width: 100%;
}

/* Style vidéo */
.video {
  height: 100%;
  aspect-ratio: 5 / 4;
  background-color: var(--color-white);
}

/* Mise en page */
#layout-margin {
  padding: 8px 0;
}

/* Responsive */
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
