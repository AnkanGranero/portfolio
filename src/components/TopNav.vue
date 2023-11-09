<script setup>
defineEmits(['openOverlay'])
defineProps({
  msg: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="topNav">
    <img class="hamburger" src="" @click="$emit('openOverlay')" />
    <h1 class="green">{{ msg }}</h1>
    <div class="links">social media</div>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
}
.hamburger {
  height: 50px;
  width: 50px;
  background: black;
}

h3 {
  font-size: 1.2rem;
}

.topNav {
  width: 100%;
  background: red;
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 1rem;
  justify-content: space-between;
}

.topNav h1,
.topNav h3 {
  text-align: center;
}

@media (min-width: 1024px) {
}
</style>
