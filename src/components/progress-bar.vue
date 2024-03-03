<template>
  <div class="progress-bar-container">
    <div class="progress-bar" :style="{width: `${progress}`}">
    <span class="percentage">
      {{ progress }}
    </span>
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps<{
    length: number,
    progress: string
}>();
</script>

<style scoped>
    .progress-bar-container {
  position: relative;
  width: 100%; 
  height: 15px;
  background-color: #fff
}

.progress-bar {
  height: 15px; 
  color: #000;
  border: 1px solid #fff; 
  background-color: hsla(160, 100%, 37%, 1);
}

.percentage {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: block;
}
</style>