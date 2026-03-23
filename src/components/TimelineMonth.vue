<script setup>
defineProps({
  month: { type: String, required: true },
})
</script>

<template>
  <div class="timeline-item">
    <div id="timeline-wrapper">
      <div id="layout-line">
        <p>{{ month }}</p>
        <div id="line"></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
#timeline-wrapper {
  width: 140px;
}

p {
  color: var(--color-orange);
  font-family: arima, sans-serif;
  font-size: 16px;
  font-weight: 400;
  line-height: 16px;
  margin: 0;
}

/* Mise en page ligne */
#layout-line {
  display: flex;
  align-items: center;
  justify-content: end;
}

#line {
  width: 26px;
  height: 1px;
  background-color: var(--color-orange);
  margin-left: 5px;
}
</style>
