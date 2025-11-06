<script setup>
import { ref } from 'vue'

// Import des icônes pour Vite
import htmlIcon from '@/assets/icons/html.png'
import cssIcon from '@/assets/icons/css.png'
import jsIcon from '@/assets/icons/js.png'
import phpIcon from '@/assets/icons/php.png'
import sqlIcon from '@/assets/icons/sql.png'
import tsIcon from '@/assets/icons/ts.png'
import cIcon from '@/assets/icons/c.png'
import pythonIcon from '@/assets/icons/python.jpeg'
import dartIcon from '@/assets/icons/dart.png'

import tailwindIcon from '@/assets/icons/tailwindcss.png'
import vueIcon from '@/assets/icons/vue.png'
import laravelIcon from '@/assets/icons/laravel.png'
import nuxtIcon from '@/assets/icons/nuxt.png'
import flutterIcon from '@/assets/icons/flutter.png'
import nestIcon from '@/assets/icons/nest.png'
import reactIcon from '@/assets/icons/react.png'

// Skills / Langages - Mis à jour selon ton profil professionnel
const skills = ref([
  {
    id: 1,
    name: 'HTML',
    width: '95%',
    color: 'linear-gradient(to right, #e44d26, #264de4)',
    icons: [{ src: htmlIcon, alt: 'HTML' }]
  },
  {
    id: 2,
    name: 'CSS / TailwindCSS',
    width: '95%',
    color: 'linear-gradient(to right, #264de4, #38bdf8)',
    icons: [{ src: cssIcon, alt: 'CSS' }]
  },
  {
    id: 3,
    name: 'JavaScript',
    width: '80%',
    color: 'linear-gradient(to right, #f7df1e, #ffe900)',
    icons: [{ src: jsIcon, alt: 'JavaScript' }]
  },
  {
    id: 4,
    name: 'TypeScript',
    width: '75%',
    color: 'linear-gradient(to right, #3178c6, #61dafb)',
    icons: [{ src: tsIcon, alt: 'TypeScript' }]
  },
  {
    id: 5,
    name: 'PHP (OO)',
    width: '90%',
    color: 'linear-gradient(to right, #8892be, #4f5b93)',
    icons: [{ src: phpIcon, alt: 'PHP' }]
  },
  {
    id: 6,
    name: 'SQL',
    width: '70%',
    color: 'linear-gradient(to right, #006494, #00c4cc)',
    icons: [{ src: sqlIcon, alt: 'SQL' }]
  },
  {
    id: 7,
    name: 'Dart',
    width: '70%',
    color: 'linear-gradient(to right, #0175c2, #42a5f5)',
    icons: [{ src: dartIcon, alt: 'Dart' }]
  }
])

// Technologies / Frameworks - Mis à jour selon ton profil professionnel
const techs = ref([
  {
    id: 1,
    name: 'Tailwind CSS',
    width: '95%',
    color: 'linear-gradient(to right, #38bdf8, #0ea5e9)',
    icons: [{ src: tailwindIcon, alt: 'Tailwind CSS' }]
  },
  {
    id: 2,
    name: 'Vue.js 3',
    width: '90%',
    color: 'linear-gradient(to right, #42b883, #35495e)',
    icons: [{ src: vueIcon, alt: 'Vue 3' }]
  },
  {
    id: 3,
    name: 'Laravel (v12)',
    width: '85%',
    color: 'linear-gradient(to right, #ff2d20, #ff7c68)',
    icons: [{ src: laravelIcon, alt: 'Laravel' }]
  },
  {
    id: 4,
    name: 'Nuxt.js',
    width: '70%',
    color: 'linear-gradient(to right, #00dc82, #2f855a)',
    icons: [{ src: nuxtIcon, alt: 'Nuxt 3' }]
  },
  {
    id: 5,
    name: 'Flutter',
    width: '70%',
    color: 'linear-gradient(to right, #02569B, #13B9FD)',
    icons: [{ src: flutterIcon, alt: 'Flutter' }]
  },
  {
    id: 6,
    name: 'NestJS',
    width: '65%',
    color: 'linear-gradient(135deg, #E0234E, #FF416C)',
    icons: [{ src: nestIcon, alt: 'Nest JS' }]
  },
  {
    id: 7,
    name: 'React.js',
    width: '50%',
    color: 'linear-gradient(to right, #61dafb, #1f2937)',
    icons: [{ src: reactIcon, alt: 'React JS' }]
  }
])
</script>

<template>
  <section class="text-white mt-10" id="skills">
    <!-- Effets de fond -->
    <div class="absolute right-0 top-[110rem] w-full h-full justify-end z-0">
      <span class="flex opacity-20">
        <span class="h-16 w-32 rounded-l-full bg-amber-500 blur-2xl"></span>
        <span class="h-16 w-32 rounded-r-full bg-pink-300 blur-2xl"></span>
      </span>
    </div>

    <!-- Contenu principal -->
    <div class="relative md:grid md:grid-cols-2 gap-8 items-center py-8 px-4 xl:gap-16 xl:px-16 z-10">

      <!-- Langages -->
      <div class="text-left flex flex-col w-full">
        <h2 class="text-4xl font-bold mb-4">
          Mes
          <span class="text-transparent bg-clip-text bg-gradient-to-r from-amber-500 to-pink-500">Langages maîtrisés</span>
        </h2>
        <div
          v-for="skill in skills"
          :key="skill.id"
          class="mt-6"
          data-aos="fade-right"
        >
          <div class="flex items-center justify-between">
            <div class="flex items-center gap-2">
              <span v-for="(icon, index) in skill.icons" :key="index">
                <img :src="icon.src" :alt="icon.alt" class="w-6 h-6" />
              </span>
              <h4 class="font-semibold">{{ skill.name }}</h4>
            </div>
            <h3 class="font-bold text-2xl">{{ skill.width }}</h3>
          </div>
          <div class="w-full h-2 mt-2 bg-[#02062b] rounded-full">
            <div
              class="h-2 rounded-full"
              :style="`width: ${skill.width}; background: ${skill.color}`"
            ></div>
          </div>
        </div>
      </div>

      <!-- Frameworks / Technologies -->
      <div class="text-left flex flex-col w-full">
        <h2 class="text-4xl font-bold mb-4">
          Mes
          <span class="text-transparent bg-clip-text bg-gradient-to-r from-amber-500 to-pink-500">Technologies</span>
        </h2>
        <div
          v-for="tech in techs"
          :key="tech.id"
          class="mt-6"
          data-aos="fade-left"
        >
          <div class="flex items-center justify-between">
            <div class="flex items-center gap-2">
              <span v-for="(icon, index) in tech.icons" :key="index">
                <img :src="icon.src" :alt="icon.alt" class="w-6 h-6" />
              </span>
              <h4 class="font-semibold">{{ tech.name }}</h4>
            </div>
            <h3 class="font-bold text-2xl">{{ tech.width }}</h3>
          </div>
          <div class="w-full h-2 mt-2 bg-[#02062b] rounded-full">
            <div
              class="h-2 rounded-full"
              :style="`width: ${tech.width}; background: ${tech.color}`"
            ></div>
          </div>
        </div>
      </div>

    </div>
  </section>
</template>
