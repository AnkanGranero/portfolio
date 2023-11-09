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
    <h1 class="green"></h1>
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
  width: 50px;
  background: $purple;
}

.topNav {
  width: 100%;
  background: $purple;
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 1rem 4%;
  justify-content: space-between;
  height: 70px;
}

.links {
  display: flex;
  /* position: relative; */
  justify-content: space-between;
  width: 17%;
  height: 100%;
  a {
    cursor: pointer;
    img {
      height: 100%;
    }
  }
}

@media (min-width: 1024px) {
}
</style>
