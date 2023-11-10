<script setup>
import { onMounted, ref } from 'vue'
import fetchFromContentful from '@/helpers/helperFunctions'

defineEmits(['openOverlay'])
defineProps({
  msg: {
    type: String,
    required: true
  }
})
const headerMenuLinks = ref()
onMounted(async () => {
  try {
    await fetchFromContentful('andreasHeaderLinks').then((resp) => {
      headerMenuLinks.value = resp.map((item) => {
        const destructedItem = item.fields
        destructedItem.image = item.fields.image.fields.file.url
        return destructedItem
      })
    })
  } catch (error) {
    throw error
  }
})
</script>

<template>
  <div class="topNav">
    <img class="hamburger" src="@/assets/menu-burger.svg" @click="$emit('openOverlay')" />
    <h1 class="name">Andreas Granér</h1>
    <div class="links">
      <a v-for="image in headerMenuLinks" :key="image.name" :href="image.url">
        <img :src="image.image" alt="" />
      </a>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.hamburger {
  height: 50px;
  width: 10%;
  margin-left: 4%;
  z-index: 2;
  cursor: pointer;

  /*   filter: invert(70%) sepia(44%) saturate(4331%) hue-rotate(229deg) brightness(100%) contrast(104%);
  filter: invert(81%) sepia(4%) saturate(5576%) hue-rotate(176deg) brightness(103%) contrast(99%);
  filter: invert(98%) sepia(2%) saturate(0%) hue-rotate(247deg) brightness(104%) contrast(102%); */
}
.name {
  color: black;
  font-weight: 300;
  position: absolute;
  width: 100%;
  text-align: center;
  letter-spacing: 3px;
  font-size: 1.5rem;
  margin-left: 4%;
}

.topNav {
  width: 100%;
  background: $topNav;
  background: white;
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 1rem 0;
  justify-content: space-between;
  height: 70px;
}

.links {
  display: none;
  /* position: relative; */
  justify-content: space-between;
  width: 17%;
  height: 100%;
  margin-right: 4%;

  a {
    cursor: pointer;
    z-index: 2;
    img {
      height: 100%;
    }
  }
}

@media (min-width: 1024px) {
  .hamburger {
    height: 50px;
    width: 50px;
    margin-left: 4%;
    z-index: 2;
    cursor: pointer;

    /*   filter: invert(70%) sepia(44%) saturate(4331%) hue-rotate(229deg) brightness(100%) contrast(104%);
  filter: invert(81%) sepia(4%) saturate(5576%) hue-rotate(176deg) brightness(103%) contrast(99%);
  filter: invert(98%) sepia(2%) saturate(0%) hue-rotate(247deg) brightness(104%) contrast(102%); */
  }
  .name {
    font-size: 2em;
    margin-left: 0;
  }

  .topNav {
    width: 100%;
    background: $topNav;
    background: $coldPurple;
    display: flex;
    flex-direction: row;
    align-items: center;
    padding: 1rem 0;
    justify-content: space-between;
    height: 70px;
  }

  .links {
    display: flex;
    /* position: relative; */
    justify-content: space-between;
    width: 17%;
    height: 100%;
    margin-right: 4%;
    a {
      cursor: pointer;
      z-index: 2;
      img {
        height: 100%;
      }
    }
  }
}
</style>
