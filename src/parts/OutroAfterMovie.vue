<script setup></script>

<template>
  <div class="screen">
    <div class="outro-movie-line-container">
      <div class="outro-movie-video-container">
        <h3>Retour en image</h3>
        <video src="/zonta-aftermovie-web.mp4" controls></video>
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
  padding: 60px 0;
}

/* Font */
h3 {
  color: var(--color-white);
  text-align: end;
  width: auto;
  white-space: nowrap;
  margin: 0;
}

.outro-movie-line-container {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}

.outro-movie-video-container {
  display: flex;
  flex-flow: row nowrap;
  max-width: 100%;
  max-height: 100%;
  gap: 20px;
}

/* Style vidéo */
video {
  flex: 1;
  min-width: 0;
  max-height: 100%;
  object-fit: cover;
  background-color: var(--color-white);
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

  video {
    flex: 1;
    min-width: 0;
    max-width: 100%;
    background-color: var(--color-white);
  }

  .outro-movie-video-container {
    flex-flow: column nowrap;
    align-items: flex-start;
    max-width: 100%;
  }
}
</style>
