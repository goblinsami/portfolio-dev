<template>
  <main>
    <section class="nav">
      <nav :class="{ 'scroll-down': isScrolled }" class="q-pa-md bar row">
        <q-btn @click="scrollToSection(button)" flat class=" cursor-pointer" v-for="button in buttons" :key="button">{{
          button }}</q-btn>
        <q-space />
        <q-btn flat class="cursor-pointer align-self-end" @click="toggleDark" size="md"
          icon="settings_brightness"></q-btn>
      </nav>
    </section>
    <section id="home" class="container">
      <div class="container row justify-center items-center text-center header">
        <div class="text-positive justify-center">
          <h1 class="text-white q-ma-none">Sami Janafse</h1><br />
          <h2 class="q-ma-none">FrontEnd Developer</h2>
          <div class="q-py-lg row justify-center items-center">
            <img src="src/assets/vue_logo.png" alt="Vue.js" class="stack-img q-pr-sm" />
            <img src="src/assets/angular_logo.png" alt="Angular" class="ang-img q-pr-sm" />
            <img src="src/assets/react_icon.png" alt="react" class="stack-img q-pr-sm" />
            <img src="src/assets/rails_icon.png" alt="Ruby on Rails" class="stack-img" />
          </div>
          <div class="q-py-md">
            <q-btn outline class=" q-mx-md" @click="scrollToSection(button)" v-for=" button  in  buttons.slice(1)"
              :key="button">{{
                button }}</q-btn>
          </div>
        </div>
      </div>
    </section>
    <section id="projects" class="projects-container">
      <!-- carousels -->
      <section class="">
        <h3 class="col-12 text-center q-my-sm">Projects</h3>
        <div class="q-pa-md col-8">
          <ProjectItem v-for=" project  in  projects " :project="project" :key="project" />
        </div>
      </section>
    </section>
    <section id="about" class="about-container row text-center justify-center">
      <!-- form to contact -->
      <h3 class="q-mb-sm" style="height: 0px;">About</h3>

      <div class="row justify-start items-center col-12">
        <img src="src/assets/vue_logo.png" alt="Vue.js" class="stack-img q-pr-sm" />
        <img src="src/assets/angular_logo.png" alt="Angular" class="ang-img q-pr-sm" />
        <img src="src/assets/react_icon.png" alt="react" class="stack-img q-pr-sm" />
        <img src="src/assets/rails_icon.png" alt="Ruby on Rails" class="stack-img" />
      </div>
      <div class="row">
        <div class="col-8">
          <p v-html="aboutText[0]"></p>
          <p v-html="aboutText[1]"></p>
          <p v-html="aboutText[3]"></p>
          <p v-html="aboutText[2]"></p>

        </div>
        <div class="col-4">
          <img src="src/assets/foto_perfil.png" alt="profile_pic" class="profile-img q-pl-md" />
        </div>
      </div>

    </section>
  </main>
</template>

<script setup >
import { ref, onMounted, onBeforeUnmount } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'
import { useQuasar } from 'quasar'
import ProjectItem from 'components/ProjectItem.vue'
const buttons = ref(['Home', 'Projects', 'About'])

const slide = ref(1)

const aboutText = ['With 3 years of experience as a front-end developer, I have worked extensively with the three major JavaScript frameworks: <b>Vue</b>, <b>Angular</b>, and <b>React</b>. Additionally, I have developed full-stack applications using <b>Ruby on Rails</b>, which has provided me with backend and database management knowledge.',
  'I have a diverse professional background, including freelance work, collaborating with technology consulting firms to build custom applications, and contributing to large companies by maintaining and enhancing existing applications. I am also experienced in implementing unit and end-to-end tests using tools like <b>Jest</b>, <b>Cypress</b>, <b>Jasmine</b> and <b>Karma</b> to ensure code security.', 'Currently based in Barcelona, I enjoy attending blues concerts and comedy shows during my free time.', 'My strengths lie in creating <b>reusable components</b>, designing intuitive user interfaces, communicating effectively, and providing elegant and efficient solutions to various challenges. If you are interested in my services, please feel free to visit my LinkedIn profile for more information and request my curriculum.']



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
const projects = [
  {
    title: 'The Sensory Lab',
    caption: 'quasar.dev',
    icon: 'school',
    description: "Maintenance of large Vue, Angular, and React projects. TSlab is a marketing company specializing in creating background music and in-store announcements, so the frontend was connected to an IoT backend using Ruby on Rails and Node. The challenge was to implement new features in the application, migrate APIs from one language to another, implement unit and end-to-end tests, and introduce state management to reduce database queries.",
    images: [{ name: 1, url: 'https://dam.malt.com/d9aad559-fc59-4cc3-a9bb-820063dcfc9e?func=bound&w=2048&org_if_sml=1' }, { name: 2, url: 'https://dam.malt.com/2c2cfeea-cce9-4d50-9e6f-47b79ccafd1c?func=bound&w=2048&org_if_sml=1' }, { name: 3, url: 'https://dam.malt.com/10f11de3-7395-43e0-9bd7-a1338bf683a9?func=bound&w=2048&org_if_sml=1' }]
  },
  {
    title: 'Tattoo Me',
    caption: 'quasar.dev',
    description: "A tattoo directory covering Belgium, France, and Spain, with a substantial database of records. The project presented the challenge of migrating a PHP-based system to Ruby on Rails while preserving the impeccable design and bolstering code security through comprehensive testing. Adapting the existing functionality to a different language was a demanding endeavor, but leveraging Test-Driven Development (TDD) allowed for efficient progress, ensuring that all client requirements and instructions were met without any setbacks.",
    icon: 'school',
    images: [{ name: 1, url: 'https://dam.malt.com/1b16481b-2666-4a74-9e7d-8821c9e6bd37?func=bound&w=2048&org_if_sml=1' }, { name: 2, url: 'https://dam.malt.com/0acad9e0-9a60-48d1-89e2-096278ad174d?func=bound&w=2048&org_if_sml=1' }, { name: 3, url: 'https://dam.malt.com/e19e6aaf-a764-4126-9b22-41486cf99181?func=bound&w=2048&org_if_sml=1' }]
  },
  {
    title: 'Idealement',
    caption: 'quasar.dev',
    description: " A fintech website that offers mortgage calculation and enables users to explore properties that are either under construction or vacant land. One of the key challenges was implementing a fresh design in specific sections of the application while also adjusting tests to accommodate the new features. Emphasizing data visualization was crucial for this project since one of its core functions revolved around presenting data. By ensuring accurate and effective data visualization, users can make better-informed decisions, ultimately adding significant value to the product.",
    icon: 'school',
    images: [{ name: 1, url: 'https://dam.malt.com/3d232806-7212-4c31-97bc-50a3473673bd?func=bound&w=2048&org_if_sml=1' }, { name: 2, url: 'https://dam.malt.com/3f2ce716-c161-4678-b519-3164b7aeccf8?func=bound&w=2048&org_if_sml=1' }, { name: 3, url: 'https://dam.malt.com/1a103350-dba5-470d-baf2-fc10cf85afeb?func=bound&w=2048&org_if_sml=1' }]
  },
  {
    title: 'Home Finance',
    caption: 'quasar.dev',
    description: "A Vue application for tracking household expenses, allowing sorting of expenses by category, price, and date, with complete CRUD operations for expenses and categories. It features a modern style with smooth and seamless transitions.",
    icon: 'school',
    images: [{ name: 1, url: 'https://dam.malt.com/4596bcfe-0176-4cf7-88eb-130940fa862a?func=bound&w=2048&org_if_sml=1' }, { name: 2, url: 'https://dam.malt.com/4d044cc9-6bc3-4e82-9a19-13ea020cefa3?func=bound&w=2048&org_if_sml=1' }, { name: 3, url: 'https://dam.malt.com/e823c3cb-24d2-45d6-a899-22346774707d?func=bound&w=2048&org_if_sml=1' }]
  },
  {
    title: 'Kitchen Genius',
    caption: 'quasar.dev',
    description: "A Vue application that incorporates ChatGPT's artificial intelligence to help you brainstorm culinary recipes. You input a maximum of 5 ingredients, and it generates a recipe that you can share on social media. In the future, additional features will be added to accommodate ingredient selection for people with food intolerances.",
    icon: 'school',
    images: [{ name: 1, url: 'https://dam.malt.com/4abbf498-c9a5-41db-a493-1acc77b02603?func=bound&w=2048&org_if_sml=1' }]
  },


]

const isScrolled = ref(false);



onMounted(() => {
  $q.dark.set(true), window.addEventListener('scroll', handleScroll);

})
onBeforeUnmount(() => {
  window.removeEventListener('scroll', handleScroll);
});

const handleScroll = () => {
  isScrolled.value = window.scrollY > 0;
};

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


const scrollToSection = (section) => {
  let sectionName = section.toLowerCase()
  console.log(sectionName)
  if (sectionName === 'home') {
    window.scrollTo({
      top: -50,
      left: 0,
      behavior: 'smooth',
    });
  } else {
    document.getElementById(sectionName).scrollIntoView({
      behavior: 'smooth',
    })
  }
}

</script>
<style lang="scss">
body {
  font-family: 'Roboto'

}

.container {
  height: 100vh;
}

.stack-img {
  height: 50px;
}

.ang-img {
  height: 60px;
}

.profile-img {
  height: 280px;
  border-radius: 50%;
}

.projects-container {
  max-width: 800px;
  display: flex;
  margin: 0 auto;
}

.about-container {
  height: 100vh;

  max-width: 800px;
  display: flex;
  margin: 0 auto;
  text-align: justify;
}

.nav {
  position: sticky;
  top: 0;
  z-index: 10;

  @media (max-width: 1340px) {
    // Estilos para anchura de pantalla menor a 1340px
    // Puedes agregar aquí los estilos que deseas aplicar

    // Ejemplo:
    background-color: rgba(23, 131, 48, 0.7) !important;
    color: white;
    font-size: 18px;
  }
}

body.body--light {
  background: #f5f5f5;

  h1 {
    color: var(--q-dark-positive) !important
  }

  .bar {
    color: var(--q-dark-positive) !important;
  }

}

nav .scroll-down {
  background-color: rgba(23, 131, 48, 0.7) !important;
  /* Cambia el color de fondo y ajusta la opacidad según sea necesario */
  transition: background-color 0.3s ease;
  /* Agrega una transición suave */
}
</style>
