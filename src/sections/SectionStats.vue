<script setup>
import StatsStatistics from './../parts/StatsStatistics.vue'
import StatsHighlightedMessage from './../parts/StatsHighlightedMessage.vue'
import StatsRecurringMessages from './../parts/StatsRecurringMessages.vue'
import StatsAllMessages from './../parts/StatsAllMessages.vue'
import StatsScrollBg from './../parts/StatsScrollBg.vue'
</script>

<template>
  <div id="burger-recapitulatif" class="burger-blue timeline-parent-position">
    <div class="container">
      <StatsStatistics></StatsStatistics>
    </div>

    <div class="container">
      <StatsHighlightedMessage></StatsHighlightedMessage>
    </div>

    <div class="container">
      <StatsRecurringMessages></StatsRecurringMessages>
    </div>

    <div class="container">
      <StatsAllMessages></StatsAllMessages>
    </div>

    <StatsScrollBg></StatsScrollBg>
  </div>
</template>

<style scoped></style>
