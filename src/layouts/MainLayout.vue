<template>
  <main>
    <section id="nav">
      <q-bar class="q-pa-lg bg-positive" style="background-color: #051c0a;">
        <q-btn flat class="cursor-pointer">File</q-btn>
        <q-btn flat class="cursor-pointer q-mx-md">Edit</q-btn>
        <q-btn flat class="cursor-pointer">View</q-btn>
        <q-btn flat class="cursor-pointer" @click="toggleDark">toggle</q-btn>
        <q-space />
      </q-bar>
      <section id="header">
        <div class="container row justify-center items-center text-center"
          style="border: 1px black solid; background-color: #051c0a;">
          <div class="text-positive justify-center">
            <h1 class="text-white q-ma-none">Sami Janafse</h1><br />
            <h2 class="q-ma-none">FrontEnd Developer</h2>
            <q-btn>Projects</q-btn>
            <q-btn>About</q-btn>
          </div>
        </div>
      </section>
    </section>
    <section id="projects">
      <h3>Projects</h3>
      <section class="row justify-center">
        <div class="q-pa-md col-8">
          <q-carousel animated v-model="slide" arrows navigation infinite>
            <q-carousel-slide :name="1" img-src="https://cdn.quasar.dev/img/mountains.jpg" />
            <q-carousel-slide :name="2" img-src="https://cdn.quasar.dev/img/parallax1.jpg" />
            <q-carousel-slide :name="3" img-src="https://cdn.quasar.dev/img/parallax2.jpg" />
            <q-carousel-slide :name="4" img-src="https://cdn.quasar.dev/img/quasar.jpg" />
          </q-carousel>
        </div>
      </section>
    </section>
    <section id="about">
      <h3>About</h3>
    </section>
  </main>
</template>

<script setup >
import { ref, onMounted } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'
import { useQuasar } from 'quasar'

const slide = ref(1)
const linksList = [
  {
    title: 'Docs',
    caption: 'quasar.dev',
    icon: 'school',
    link: 'https://quasar.dev'
  },
  {
    title: 'Github',
    caption: 'github.com/quasarframework',
    icon: 'code',
    link: 'https://github.com/quasarframework'
  },
  {
    title: 'Discord Chat Channel',
    caption: 'chat.quasar.dev',
    icon: 'chat',
    link: 'https://chat.quasar.dev'
  },
  {
    title: 'Forum',
    caption: 'forum.quasar.dev',
    icon: 'record_voice_over',
    link: 'https://forum.quasar.dev'
  },
  {
    title: 'Twitter',
    caption: '@quasarframework',
    icon: 'rss_feed',
    link: 'https://twitter.quasar.dev'
  },
  {
    title: 'Facebook',
    caption: '@QuasarFramework',
    icon: 'public',
    link: 'https://facebook.quasar.dev'
  },
  {
    title: 'Quasar Awesome',
    caption: 'Community Quasar projects',
    icon: 'favorite',
    link: 'https://awesome.quasar.dev'
  }
]


onMounted(() => {
  $q.dark.set(true)
})


const leftDrawerOpen = ref(false)
const $q = useQuasar()

// get status
console.log($q.dark.isActive) // true, false

// get configured status
console.log($q.dark.mode) // "auto", true, false

// set status
$q.dark.set(true) // or false or "auto"

// toggle
$q.dark.toggle()

const toggleDark = () => {
  $q.dark.toggle()

}

</script>
<style>
.container {
  height: 100vh
}
</style>
