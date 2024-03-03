<template>
  <div class="progress-bar-container">
    <div class="progress-bar" :style="{width: `${percentageOfProgress}`}">
    <span class="percentage">
      {{ percentageOfProgress }}
    </span>
    </div>
  </div>
</template>

<script setup lang="ts">
</script>

<style scoped>
    
</style>