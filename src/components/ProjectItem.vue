<script setup>
import { ref } from 'vue'
const props = defineProps(['project'])


const slide = ref(1)

</script>

<template>
  <main class="">

    <h4 class="q-my-md"><a target="_blank" :href="props.project.link_main"> {{ props.project.title }} </a> </h4>

    <p class="q-my-md">{{ props.project.description }}</p>
    <q-carousel :control-type="'push'" animated v-model="slide" arrows navigation infinite control-color="secondary">
      <q-carousel-slide v-for="image in props.project.images" :key="image" :name="image.name" :img-src="image.url" />
    </q-carousel>
  </main>
</template>

<style scoped>
</style>
