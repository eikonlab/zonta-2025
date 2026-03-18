<script setup></script>

<template>
  <div class="screen">
    <h2>Messages du sapin porte-paroles</h2>
    <div class="filters">
      <button @click="setFilter('support')">Soutien émotionnel</button>
      <button @click="setFilter('action')">Appel à l'action</button>
      <button @click="setFilter('solidarity')">Solidarité collective</button>
      <button @click="setFilter('condemnation')">Condamnation de la violence</button>
      <button @click="setFilter('tributes')">Hommages aux victimes</button>
    </div>
    <div class="curves-container">
      <div v-for="(curve, i) in curves" :key="i" class="curve">
        <span
          v-for="word in curve.words"
          :key="word.id"
          class="word"
          :style="{ transform: `translateX(${word.x}px)` }"
        >
          {{ word.text }}
        </span>
      </div>
    </div>
  </div>
</template>

<style scoped>
button {
  font-size: 15px;
  font-weight: 700;

  border-radius: 29px;
  padding: 3px 15px 5px;
  margin-top: 24px;

  border: 1.4px solid #8fa9c8;
  background-color: var(--color-light-blue);
  color: var(--color-blue);

  transition:
    transform 0.4s ease,
    color 0.2s ease,
    border 0.2s ease;
}

button:hover {
  color: var(--color-orange);
  border: 1.4px solid var(--color-orange);
  transform: scale(1.04);
}
</style>
