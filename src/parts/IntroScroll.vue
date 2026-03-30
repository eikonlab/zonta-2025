<script setup>
import ButtonScroll from './../components/ButtonScroll.vue'
</script>

<template>
  <div id="intro-scroll">
    <div id="position-button-scroll">
      <div id="button-parent">
        <div id="button-div">
          <ButtonScroll></ButtonScroll>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
#button-parent {
  width: 100%;
  height: 100vh;
}

#button-div {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
}

#position-button-scroll {
  width: 100%;
  height: 100vh;
  inset: 0;
  position: sticky;
}

#intro-scroll {
  position: relative;
  height: 200vh !important;
}
</style>
