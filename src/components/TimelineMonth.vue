<script setup>
defineProps({
  month: { type: String, required: true },
})
</script>

<template>
  <div>
    <div id="timeline-month-wrapper">
      <div id="timeline-month-layout-line">
        <p>{{ month }}</p>
        <div id="timeline-month-line"></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
#timeline-month-wrapper {
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
#timeline-month-layout-line {
  display: flex;
  align-items: center;
  justify-content: end;
}

#timeline-month-line {
  width: 26px;
  height: 1px;
  background-color: var(--color-orange);
  margin-left: 5px;
}
</style>
