<script setup>
defineProps({
  date: { type: String, required: true },
  location: { type: String, required: true },
  age: { type: String, required: true },
})
</script>

<template>
  <div class="timeline-item">
    <div class="timeline-wrapper">
      <div class="layout-line">
        <p class="date">{{ date }}</p>
        <div class="big-line"></div>
      </div>

      <p class="location">{{ location }}</p>

      <p class="age">
        <strong>{{ age }}</strong>
      </p>
    </div>
  </div>
</template>

<style scoped>
.timeline-wrapper {
  width: 210px;
}

p {
  color: var(--color-orange);
  font-family: arima, sans-serif;
  font-size: 16px;
  font-weight: 400;
  line-height: 16px;
  margin: 0;
}

strong {
  font-size: 15px;
  font-weight: 700;
  line-height: 16px;
}

.age {
  width: 190px;
}

/* Mise en page ligne */
.layout-line {
  display: flex;
  align-items: center;
}

.big-line {
  flex: 1;
  height: 1px;
  min-height: 1px;
  background-color: var(--color-orange);
  margin-left: 8px;
}

/* Animation apparition */
.date,
.location {
  opacity: 0;
  transform: translateY(5px);
}

.age {
  transform: translateY(-38px);
}
</style>
