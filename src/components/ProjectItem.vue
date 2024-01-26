<script setup>
import { ref, reactive } from 'vue'
const props = defineProps(['project'])


const slide = ref(1)
const tilt = reactive({
  mouseX: 0,
  mouseY: 0
});
const tiltStyle = ref({
  transform: 'rotateX(0deg) rotateY(0deg)',
  transition: 'transform 0.5s ease' // Transición suave
});
const handleMouseMove = (event) => {
  const boundingBox = event.target.getBoundingClientRect();
  tilt.mouseX = event.clientX - boundingBox.left - boundingBox.width / 2;
  tilt.mouseY = event.clientY - boundingBox.top - boundingBox.height / 2;

  tiltStyle.value.transform = `rotateX(${tilt.mouseY / 10}deg) rotateY(${tilt.mouseX / 10}deg)`;
};
const imgIndex = ref(0);
const imgID = ref(237);

const resetTilt = () => {
  tiltStyle.value.transform = 'rotateX(0deg) rotateY(0deg)';
};
</script>

<template>
  <main class="">
    <div class="title-container">
      <h4 class="q-my-md"><a target="_blank" :href="props.project.link_main"> {{ props.project.title }} </a> </h4>

      <p class="q-my-md">{{ props.project.description }}</p>

    </div>
    <q-carousel :control-type="'push'" animated v-model="slide" arrows navigation infinite control-color="secondary"
      @mousemove="handleMouseMove" :style="tiltStyle" @mouseleave="resetTilt">
      <q-carousel-slide v-for="image in props.project.images" :key="image" :name="image.name" :img-src="image.url" />
    </q-carousel>
  </main>
</template>

<style scoped>
</style>
