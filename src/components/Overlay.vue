<script setup>
defineEmits(['closeOverlay'])
</script>

<template>
  <div class="overlay" @click="$emit('closeOverlay')"></div>
</template>

<style scoped>
.overlay {
  height: 100%;
  width: 100%;
  background: black;
  position: absolute;
  top: 0;
  z-index: 2;
  opacity: 0.6;
}

@media (min-width: 1024px) {
}
</style>
