<script setup>
import { RouterLink, RouterView } from 'vue-router'
import TopNav from './components/TopNav.vue'
import Overlay from './components/Overlay.vue'
import fetchFromContentful from './helpers/helperFunctions'
import { onMounted, ref } from 'vue'

const overlayIsOpen = ref(false)
function setOverlayState(bool) {
  overlayIsOpen.value = bool
}
const portfolioImages = ref()
onMounted(async () => {
  try {
    await fetchFromContentful('andreasPortfolio').then((resp) => {
      portfolioImages.value = resp
        .map((item) => {
          const destructedItem = item.fields
          destructedItem.url = item.fields.picture.fields.file.url
          return destructedItem
        })
        .sort((a, b) => a.order - b.order)
    })
  } catch (error) {
    throw error
  }
})
</script>

<template>
  <div class="app">
    <Overlay v-if="overlayIsOpen" @closeOverlay="setOverlayState(false)" />
    <header>
      <TopNav msg="Andreas Granér" @openOverlay="setOverlayState(true)" />
      <div class="blue-line" />
    </header>
    <div class="grid-container">
      <div v-for="image in portfolioImages" :key="image.order">
        <img :src="image.url" class="gallery-img" />
      </div>
    </div>
    <footer class="footer"></footer>

    <!--  <RouterView /> -->
  </div>
</template>

<style lang="scss" >
@import url('https://fonts.googleapis.com/css2?family=Josefin+Sans:ital,wght@0,100;0,200;0,300;0,500;1,100;1,300&display=swap');
body {
  background-color: $babyBlue;
  background-color: white;
  font-family: 'Josefin Sans', sans-serif;
}
header {
  line-height: 1.5;
  max-height: 100vh;
  width: 100%;
  position: fixed;
  top: 0;
  /*   .blue-line {
    width: 100%;
    position: fixed;
    height: 0.5%;
    background-color: white;
  } */
}
.grid-container {
  width: 100%;
  display: flex;
  flex-direction: column;
  grid-gap: 5%;
  padding: 4%;
  margin-top: 18%;
  margin-bottom: 8%;

  img {
    /*     padding: 10px; */
    /* background: $blueHighlight; */
    /*    -webkit-box-shadow: 0 0 24px -9px white;
    box-shadow: 0 0 30px $blueHighlight; */
    /* box-shadow: 0px -25px 20px -20px rgba(179, 227, 254, 1),
      0px -2px 23px 15px rgba(179, 227, 254, 1), 0px 25px 20px -20px rgba(179, 227, 254, 1),
      -25px -17px 20px -20px rgba(179, 227, 254, 1); */
  }
}
.app {
  max-width: 100vw;
}
.gallery-img {
  max-width: 100%;
}
.footer {
}

@media (min-width: 1024px) {
  body {
    background-color: $babyBlue;
    font-family: 'Josefin Sans', sans-serif;
  }
  header {
    line-height: 1.5;
    max-height: 100vh;
    width: 100%;
    position: fixed;
    top: 0;
    /*   .blue-line {
    width: 100%;
    position: fixed;
    height: 0.5%;
    background-color: white;
  } */
  }
  .grid-container {
    width: 100%;
    display: grid;
    grid-template-columns: repeat(3, 30% [col-start]);
    grid-template-rows: auto;
    grid-gap: 5%;
    padding: 4%;
    margin-top: 5%;
    margin-bottom: 8%;

    img {
      /*     padding: 10px; */
      /* background: $blueHighlight; */
      -webkit-box-shadow: 0 0 24px -9px white;
      box-shadow: 0 0 30px $blueHighlight;
      /* box-shadow: 0px -25px 20px -20px rgba(179, 227, 254, 1),
      0px -2px 23px 15px rgba(179, 227, 254, 1), 0px 25px 20px -20px rgba(179, 227, 254, 1),
      -25px -17px 20px -20px rgba(179, 227, 254, 1); */
    }
  }
  .app {
    max-width: 100vw;
  }
  .gallery-img {
    max-width: 100%;
  }
  .footer {
  }
}
</style>
