<script setup>
import StatsStatistics from './../parts/StatsStatistics.vue'
import StatsHighlightedMessage from './../parts/StatsHighlightedMessage.vue'
import StatsRecurringMessages from './../parts/StatsRecurringMessages.vue'
import StatsAllMessages from './../parts/StatsAllMessages.vue'
import Timeline from './../components/Timeline.vue'
</script>

<template>
  <div id="burger-recapitulatif" class="burger-blue">
    <!-- <Timeline></Timeline> -->

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
  </div>
</template>

<style scoped></style>
