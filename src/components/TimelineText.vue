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

      <!-- <p class="age">
        <strong>{{ age }}</strong>
      </p> -->

      <div class="layout-line-age">
        <p class="age">
          <strong>{{ age }}</strong>
        </p>
        <div class="age-line"></div>
      </div>
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

.layout-line-age {
  margin-top: 4px;

  display: flex;
  align-items: flex-start;
}

/* Animation apparition */
/* .date,
.location {
  opacity: 0;
  transform: translateY(5px);
}

.age {
  transform: translateY(-38px);
} */

/* Animation apparition v2 */

/* État initial */

.age-line {
  width: 16px;
  height: 1px;
  min-height: 1px;
  background-color: var(--color-orange);
  margin-left: 4px;
  margin-top: 9px;
  transform-origin: left;

  opacity: 1;
}

.date,
.location {
  opacity: 0;
  transform: translateY(5px);
}

.big-line {
  transform-origin: left;
  opacity: 0;
}

.layout-line-age {
  transform: translateY(-38px);
  will-change: transform;
}
</style>
