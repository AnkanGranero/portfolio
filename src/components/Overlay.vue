<script setup>
defineEmits(['closeOverlay'])
</script>

<template>
  <div class="overlay" @click="$emit('closeOverlay')">
    <a href="">HOME</a>
    <a href="">ART</a>
    <a href="">MUSIC</a>
    <a href="">ABOUT</a>
  </div>
</template>

<style type="scss" scoped>
.overlay {
  height: 100%;
  width: 100%;
  background: rgb(234 129 255);
  background: white;
  background: #dba5f5;
  position: fixed;
  top: 0;
  z-index: 2;
  /* opacity: 0.8; */
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
}
a {
  color: black;
  /*   color: white;
  color: rgb(234 129 255); */
  text-decoration: none;
  font-weight: 300;
  font-size: 1.4rem;
}

@media (min-width: 1024px) {
  .overlay {
    height: 100%;
    width: 100%;
    background: black;
    /* background: rgb(234 129 255); */
    position: fixed;
    top: 0;
    z-index: 2;
    opacity: 0.8;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-evenly;
  }
  a {
    color: white;

    text-decoration: none;
    font-weight: 300;
    font-size: 1.9rem;
  }
}
</style>
