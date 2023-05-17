<script setup>
import { ref } from 'vue'
const props = defineProps(['project'])


const slide = ref(1)

</script>

<template>
  <main class="">
    <h4 class="q-my-md">{{ props.project.title }}</h4>
    <p class="q-my-md">{{ props.project.description }}</p>
    <q-carousel animated v-model="slide" arrows navigation infinite>
      <q-carousel-slide v-for="image in props.project.images" :key="image" :name="image.name" :img-src="image.url" />
    </q-carousel>
  </main>
</template>

<style scoped>
</style>
