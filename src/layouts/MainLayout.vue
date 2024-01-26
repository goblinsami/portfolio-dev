<template>
  <main>
    <section class="nav">
      <nav class="q-pa-md bar row">
        <q-btn @click="scrollToSection(button)" flat class=" cursor-pointer" v-for="button in buttons" :key="button">{{
          button }}</q-btn>
        <q-space />
        <q-btn flat class="cursor-pointer align-self-end" @click="toggleDark" size="md"
          icon="settings_brightness"></q-btn>
      </nav>
    </section>
    <section style="display: none;">
      <div class="click">
        <input type="checkbox" class="click_checkbox" />
      </div>
    </section>


    <section id="home" class="container">
      <div class="container row justify-center items-center text-center header">
        <div class="text-positive justify-center">
          <div @mousemove="handleMouseMove" :style="tiltStyle" @mouseleave="resetTilt" class="title-container">
            <h1 class="text-white q-ma-none">Sami Janafse</h1><br />
            <h2 class="q-ma-none">FrontEnd Developer</h2>
          </div>

          <div class="q-py-lg row justify-center items-center ">
            <a target="_blank" class="logo">
              <img src="~assets/vue_logo.png" alt="Vue.js" class="stack-img q-pr-md click_checkbox" href="" />
            </a>
            <a target="_blank" href="https://angular.io/" class="click">
              <img src="~assets/cropped.png" alt="Angular" class="stack-img q-pr-md click_checkbox" />
            </a>
            <a target="_blank" href="https://react.dev/" class="click">
              <img src="~assets/react_icon.png" alt="react" class="stack-img q-pr-md click_checkbox" />
            </a>
            <a target="_blank" href="https://guides.rubyonrails.org/" class="click">
              <img src="~assets/rails_icon.png" alt="Ruby on Rails" class="stack-img click_checkbox" />
            </a>
          </div>
          <!--           <section class="logo" @mouseover="startHover" @mouseout="endHover"></section>
 -->
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
        <h3 class="col-12 text-center q-my-sm text-bold">Projects</h3>
        <div class="q-pa-md col-8">
          <ProjectItem class="q-my-lg q-mb-md" v-for=" project  in  projects " :project="project" :key="project" />
        </div>
      </section>
    </section>
    <section id="about" class="about-container row text-center justify-center">
      <!-- form to contact -->
      <h3 class="q-mb-xl about-header text-bold" style="height: 0px;">About</h3>
      <!--  $q.screen.width < 1025 -->
      <div :class="'row items-end col-12 q-pb-md stack-list q-px-sm q-py-md'">
        <a target="_blank" href="https://vuejs.org/guide/introduction.html">
          <img src="~assets/vue_logo.png" alt="Vue.js" class="stack-img-mb q-pr-sm" />
        </a>
        <a target="_blank" href="https://angular.io/">
          <img src="~assets/cropped.png" alt="Angular" class="stack-img-mb q-pr-sm" />
        </a>
        <a target="_blank" href="https://react.dev/">
          <img src="~assets/react_icon.png" alt="react" class="stack-img-mb q-pr-sm" />
        </a>
        <a target="_blank" href="https://guides.rubyonrails.org/">
          <img src="~assets/rails_icon.png" alt="Ruby on Rails" class="stack-img-mb" />
        </a>

      </div>
      <div class="row items-start justify-center">
        <div class="col-12 col-md-8 q-px-sm">
          <p v-html="aboutText[0]"></p>
          <p v-html="aboutText[1]"></p>
          <p v-html="aboutText[3]"></p>
          <p v-html="aboutText[2]"></p>

        </div>
        <div class="col-12 col-md-4 text-center">
          <img src="~assets/foto_perfil.png" alt="profile_pic" class="profile-img q-pl-md" />
        </div>
      </div>

    </section>
  </main>
</template>

<script setup >
import { ref, reactive, onMounted, onBeforeUnmount } from 'vue'
import { useQuasar } from 'quasar'
import ProjectItem from 'components/ProjectItem.vue'
import { useMeta } from 'quasar'
import 'transition-style';


let hoverTimer = null;

const startHover = () => {
  // Comienza el temporizador cuando el ratón entra

  console.log('entraaaa')
  hoverTimer = setTimeout(() => {
    console.log('Ratón ha estado sobre el botón durante 1 segundo');
    document.querySelector('.logo').classList.add('click_checkbox');


  }, 600);
};

const endHover = () => {
  console.log('endHover')
  setTimeout(() => {

    document.querySelector('.logo').classList.remove('click_checkbox');
  }, 600);

  // Restablece el temporizador si el ratón sale antes de 1 segundo
  clearTimeout(hoverTimer);
};


//MOUSE HANDLERS
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
const metaData = {
  // sets document title
  title: 'Sami Janafse - FrontEnd Developer',
  // optional; sets final title as "Index Page - My Website", useful for multiple level meta

  // meta tags
}
const buttons = ref(['Home', 'Projects', 'About'])

const slide = ref(1)

const aboutText = ['With 3 years of experience as a front-end developer, I have worked extensively with the three major JavaScript frameworks: <b>Vue</b>, <b>Angular</b>, and <b>React</b>. Additionally, I have developed full-stack applications using <b>Ruby on Rails</b>, which has provided me with backend and database management knowledge.',
  'I have a diverse professional background, including freelance work, collaborating with technology consulting firms to build custom applications, and contributing to large companies by maintaining and enhancing existing applications. I am also experienced in implementing unit and end-to-end tests using tools like <b>Jest</b>, <b>Cypress</b>, <b>Jasmine</b> and <b>Karma</b> to ensure code security.', 'Currently based in Barcelona, I enjoy attending blues concerts and comedy shows during my free time.', 'My strengths lie in creating <b>reusable components</b>, designing intuitive user interfaces, communicating effectively, and providing elegant and efficient solutions to various challenges. If you are interested in my services, please feel free to visit my <b><a target="_blank" href="https://www.linkedin.com/in/sami-janafse-9a8639121/">LinkedIn profile</a></b> for more information and request my curriculum.']



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
    link_main: 'https://thesensorylab.es/',
    description: "Maintenance of large Vue, Angular, and React projects. Tslab is a marketing company specializing in creating background music and in-store announcements, so the frontend was connected to an IoT backend using Ruby on Rails and Node. The challenge was to implement new features in the application, migrate APIs from one language to another, implement unit and end-to-end tests, and introduce state management to reduce database queries.",
    images: [{ name: 1, url: 'https://dam.malt.com/d9aad559-fc59-4cc3-a9bb-820063dcfc9e?func=bound&w=2048&org_if_sml=1' }, { name: 2, url: 'https://dam.malt.com/2c2cfeea-cce9-4d50-9e6f-47b79ccafd1c?func=bound&w=2048&org_if_sml=1' }, { name: 3, url: 'https://dam.malt.com/10f11de3-7395-43e0-9bd7-a1338bf683a9?func=bound&w=2048&org_if_sml=1' }]
  },
  {
    title: 'Tattoo Me',
    caption: 'quasar.dev',
    link_main: 'https://www.tattoome.com/',
    description: "A tattoo directory covering Belgium, France, and Spain, with a substantial database of records. The project presented the challenge of migrating a PHP-based system to Ruby on Rails while preserving the impeccable design and bolstering code security through comprehensive testing. Adapting the existing functionality to a different language was a demanding endeavor, but leveraging Test-Driven Development (TDD) allowed for efficient progress, ensuring that all client requirements and instructions were met without any setbacks.",
    icon: 'school',
    images: [{ name: 1, url: 'https://dam.malt.com/1b16481b-2666-4a74-9e7d-8821c9e6bd37?func=bound&w=2048&org_if_sml=1' }, { name: 2, url: 'https://dam.malt.com/0acad9e0-9a60-48d1-89e2-096278ad174d?func=bound&w=2048&org_if_sml=1' }, { name: 3, url: 'https://dam.malt.com/e19e6aaf-a764-4126-9b22-41486cf99181?func=bound&w=2048&org_if_sml=1' }]
  },
  {
    title: 'Idealement',
    caption: 'quasar.dev',
    link_main: 'https://www.idealement.fr/',
    description: " A fintech website that offers mortgage calculation and enables users to explore properties that are either under construction or vacant land. One of the key challenges was implementing a fresh design in specific sections of the application while also adjusting tests to accommodate the new features. Emphasizing data visualization was crucial for this project since one of its core functions revolved around presenting data. By ensuring accurate and effective data visualization, users can make better-informed decisions, ultimately adding significant value to the product.",
    icon: 'school',
    images: [{ name: 1, url: 'https://dam.malt.com/3d232806-7212-4c31-97bc-50a3473673bd?func=bound&w=2048&org_if_sml=1' }, { name: 2, url: 'https://dam.malt.com/3f2ce716-c161-4678-b519-3164b7aeccf8?func=bound&w=2048&org_if_sml=1' }, { name: 3, url: 'https://dam.malt.com/1a103350-dba5-470d-baf2-fc10cf85afeb?func=bound&w=2048&org_if_sml=1' }]
  },


  {
    title: 'Freelance Projects',
    caption: 'quasar.dev',
    description: "Some of my freelance and personal projects. Home Finance: A Vue application for tracking household expenses, allowing sorting of expenses by category, price, and date, with complete CRUD operations for expenses and categories. It features a modern style with smooth and seamless transitions. Kitchen Genius: A Vue application that incorporates ChatGPT's artificial intelligence to help you brainstorm culinary recipes. You input a maximum of 5 ingredients, and it generates a recipe that you can share on social media. In the future, additional features will be added to accommodate ingredient selection for people with food intolerances.",
    icon: 'school',
    images: [{ name: 1, url: 'https://dam.malt.com/bba8f110-6413-4b2e-938d-e5e4db66edd0?func=bound&w=2048&org_if_sml=1' }, { name: 2, url: 'https://dam.malt.com/9a636687-4d2b-4f6d-b954-ae8378924dda?func=bound&w=2048&org_if_sml=1' }]
  },


]

const isScrolled = ref(false);



onMounted(() => {
  $q.dark.set(true), useMeta(metaData);

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
@import "transition-style";

@keyframes circle-swoop {
  from {
    clip-path: var(--circle-top-right-out);
  }

  to {
    clip-path: var(--circle-bottom-right-in);
  }
}

.--in-custom {
  --transition__duration: 1s;
  --transition__easing: ease-in-out;
  animation-name: circle-swoop;
}



body {
  font-family: 'Roboto'

}

.container {
  height: 100vh;
}

.stack-img {
  height: 50px;
}




.stack-img-mb {
  height: 50px;

  @media (max-width: 1340px) {
    height: 30px;

  }
}

.--in-custom {
  --transition__duration: 1s;
  --transition__easing: ease-in-out;
  animation-name: square-in-hesitate;
}

@keyframes square-in-hesitate {
  0% {
    clip-path: inset(100% 100% 100% 100%);
  }

  40% {
    clip-path: inset(33% 33% 33% 33%);
  }

  100% {
    clip-path: inset(0 0 0 0);
  }
}

[transition-style="in:square:hesitate"] {
  animation: 2.5s cubic-bezier(.25, 1, .30, 1) square-in-hesitate both;
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

body.body--dark {
  background: var(--q-dark-page);
  //animation: backgroundColorPalette 20s infinite;

}

@keyframes backgroundColorPalette {
  0% {
    background: var(--q-dark-page)
  }

  50% {
    background: #11355c
  }

  100% {
    background: var(--q-dark-page)
  }
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

  a {
    text-decoration: none !important;
    color: rgb(0, 0, 0)
  }

  h1 {
    color: var(--q-dark-positive) !important
  }

  .bar {
    color: var(--q-dark-positive) !important;
  }

}

a {
  text-decoration: none !important;
  color: white
}

// CLICK

.click {
  perspective: 300px;

  &_checkbox {
    appearance: none;
    display: block;


    animation-name: elastic-clickOn;
    animation-duration: 1.8s;
    animation-fill-mode: forwards;
    animation-timing-function: ease-in-out;
    transform-style: preserve-3d;

    &:hover {
      animation-name: elastic-clickOff;
    }

    &::before {
      position: absolute;
      top: 0%;
      left: 0%;
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      transform: translateZ(0.5em);
      backface-visibility: hidden;
    }

    &::after {
      position: absolute;
      top: 0%;
      left: 0%;
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      color: #fff;
      transform: rotateX(180deg) translateZ(0.5em);
      backface-visibility: hidden;
    }

    @keyframes elastic-clickOff {
      0% {
        transform: rotateX(0deg);
      }

      28.22% {
        transform: rotateX(218.76deg);
      }

      48.82% {
        transform: rotateX(152.36deg);
      }

      63.85% {
        transform: rotateX(199.52deg);
      }

      74.83% {
        transform: rotateX(166.41deg);
      }

      82.84% {
        transform: rotateX(189.27deg);
      }

      88.68% {
        transform: rotateX(173.89deg);
      }

      92.95% {
        transform: rotateX(183.81deg);
      }

      96.07% {
        transform: rotateX(177.88deg);
      }

      98.34% {
        transform: rotateX(180.90deg);
      }

      100.00% {
        transform: rotateX(180.00deg);
      }
    }

    @keyframes elastic-clickOn {
      0% {
        transform: rotateX(180deg);
      }

      28.22% {
        transform: rotateX(398.76deg);
      }

      48.82% {
        transform: rotateX(332.36deg);
      }

      63.85% {
        transform: rotateX(379.52deg);
      }

      74.83% {
        transform: rotateX(346.41deg);
      }

      82.84% {
        transform: rotateX(369.27deg);
      }

      88.68% {
        transform: rotateX(353.89deg);
      }

      92.95% {
        transform: rotateX(363.81deg);
      }

      96.07% {
        transform: rotateX(357.88deg);
      }

      98.34% {
        transform: rotateX(360.90deg);
      }

      100.00% {
        transform: rotateX(360.00deg);
      }
    }
  }
}

// CHECKBOX

.check {
  position: relative;
  display: inline-block;

  &_checkbox {
    appearance: none;

  }

  &_checkbox:checked~&_on {
    animation-name: none;
    z-index: 1;
  }

  &_checkbox:checked~&_off {
    animation-name: elastic-check;
    z-index: 2;
  }

  &_on,
  &_off {
    position: absolute;
    left: -1em;
    top: 50%;
    width: 1em;
    height: 1em;
    transform: translateY(-50%);
    animation-duration: 1s;
    animation-fill-mode: forwards;
    animation-timing-function: ease-in-out;
  }

  &_on {
    background-color: red;
    animation-name: elastic-check;
    z-index: 2;
  }

  &_off {
    background-color: #777;
    animation-name: none;
    z-index: 1;
  }

  @keyframes elastic-check {
    0% {
      transform: translateY(-50%) scale(0);
    }

    49.91% {
      transform: translateY(-50%) scale(1.38);
    }

    75.12% {
      transform: translateY(-50%) scale(0.81);
    }

    87.85% {
      transform: translateY(-50%) scale(1.09);
    }

    94.28% {
      transform: translateY(-50%) scale(0.96);
    }

    97.53% {
      transform: translateY(-50%) scale(1.02);
    }

    99.17% {
      transform: translateY(-50%) scale(0.99);
    }

    100.00% {
      transform: translateY(-50%) scale(1.00);
    }
  }
}
</style>
