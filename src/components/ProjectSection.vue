<template>
  <section class="text-white mt-20 bg-gradient-to-br from-[#1e293b] via-[#111a2e] to-[#0f172a]" id="projects">
    <div class="px-4 xl:pl-16">
      <!-- Header -->
      <div class="mb-4 flex flex-col md:flex-row md:justify-between md:items-center xl:pr-16">
        <h2 class="text-white font-bold text-4xl drop-shadow-lg mb-4 md:mb-0">
          Mes <span class="text-transparent bg-clip-text bg-gradient-to-r from-orange-400 via-pink-500 to-purple-600">Projets professionnels</span>
        </h2>

        <!-- Categories -->
        <div class="flex flex-wrap md:flex-nowrap gap-2 md:gap-4 z-10 relative">
        <button
            v-for="category in categories"
            :key="category.name"
            @click="selectedCategory = category.name"
            class="px-4 py-2 sm:px-6 sm:py-3 rounded-lg transition-all duration-200 font-semibold border border-transparent focus:outline-none relative z-10"
            :class="selectedCategory === category.name
            ? 'bg-gradient-to-r from-orange-400 to-pink-500 text-white shadow-lg'
            : 'bg-[#1e293b] text-gray-300 hover:border-orange-400 hover:bg-gradient-to-r hover:from-orange-400 hover:to-pink-500 hover:text-white'"
        >
            {{ category.name }} ({{ category.count }})
        </button>
        </div>

      </div>


    <div class="relative mt-10 flex items-center justify-center w-445">
    <!-- Bouton gauche -->
    <button
        @click="scrollPrev"
        class="absolute -left-10 md:-left-14 bg-gradient-to-r from-orange-500 to-pink-500 text-white text-2xl w-12 h-12 flex justify-center items-center rounded-full shadow-lg hover:scale-110 transition-all duration-300"
    >
        <i class="fas fa-chevron-left"></i>
    </button>

    <!-- Conteneur scrollable -->
    <div
        ref="scrollContainer"
        class="flex space-x-8 overflow-x-scroll scroll-smooth scrollbar-hide px-4 md:px-10"
        @mouseenter="pauseScroll"
        @mouseleave="resumeScroll"
    >
        <div
        v-for="(project, idx) in infiniteProjects"
        :key="project.id + '-' + idx"
        class="w-[320px] md:w-[360px] lg:w-[400px] flex-shrink-0"
        >
        <ProjectCard :project="project" />
        </div>
    </div>

    <!-- Bouton droit -->
    <button
        @click="scrollNext"
        class="absolute right-20 md:-right-14 bg-gradient-to-r from-orange-500 to-pink-500 text-white text-2xl w-12 h-12 flex justify-center items-center rounded-full shadow-lg hover:scale-110 transition-all duration-300"
    >
        <i class="fas fa-chevron-right"></i>
    </button>
    </div>

    </div>
  </section>
</template>

<script setup>
import { ref, computed, onMounted, onBeforeUnmount, watch, nextTick } from 'vue'
import ProjectCard from './ProjectCard.vue'
import VueImage from '../assets/icons/cd.png'
import EE from '../assets/ee.png'
import Sie from '../assets/icons/sie.png'
import logoImage from '../assets/icons/logo.png'
import DevelopmentImage from '../assets/development.webp'

const projects = ref([
  {
    id: 1,
    category: 'Développement Web',
    name: 'Civil Design',
    image: VueImage,
    description:
      'Civil Design est une plateforme complète permettant la vente de plans de maisons ainsi que des formations aux logiciels Autodesk.',
    technologie: ['Laravel', 'Vue.js 3', 'TypeScript', 'TailwindCSS', 'MySQL']
  },
  {
    id: 2,
    category: 'Développement Web',
    name: 'SIE',
    image: Sie,
    description:
      'Plateforme permettant de gerer les procedures d\'obtention de visa.',
    technologie: ['Laravel', 'Vue.js 3', 'TypeScript', 'TailwindCSS', 'MySQL']
  },
  {
    id: 3,
    category: 'Développement Web',
    name: 'Site Epreuves-Examens',
    image: EE,
    description:
      'Plateforme pour accéder et acheter les épreuves des examens officiels passés.',
    technologie: ['Laravel', 'Vue.js 3', 'TypeScript', 'TailwindCSS', 'MySQL']
  },
  { id: 4, category: 'Développement Web', name: 'Site DevPerso', image: DevelopmentImage, description: 'Bibliothèque en ligne avec vente de livres et gestion des utilisateurs. CRUD complet sur livres et utilisateurs, paiement simple et interface intuitive.', technologie: ['PHP POO', 'MySQL', 'HTML', 'CSS', 'Bootstrap'] },
  {
    id: 5,
    category: 'Outils Web',
    name: 'Mini Calco',
    image: logoImage,
    description:
      'Application web pour effectuer des calculs complexes avec interface fluide.',
    technologie: ['HTML', 'CSS', 'JavaScript']
  },
  {
    id: 6,
    category: 'IA/Full-Stack',
    name: 'Mini Chatbot AI',
    image: logoImage,
    description:
      'Chatbot intelligent répondant aux questions des utilisateurs en temps réel.',
    technologie: ['NestJS', 'React JS', 'JavaScript']
  },
  { id: 7, category: 'Outils Web', name: 'Mini Calendar', image: logoImage, description: 'Fournit le calendrier exact pour un nombre de mois précis. Gère les décalages, années bissextiles et affichage clair sans utiliser l’objet Date.', technologie: ['HTML', 'CSS', 'JavaScript'] }
])

const selectedCategory = ref('Tous')
const scrollContainer = ref(null)
let scrollInterval = null
let isPaused = false

// === Génération dynamique des catégories ===
const categories = computed(() => {
  const map = projects.value.reduce((acc, p) => {
    acc[p.category] = (acc[p.category] || 0) + 1
    return acc
  }, {})
  return [{ name: 'Tous', count: projects.value.length }].concat(
    Object.entries(map).map(([name, count]) => ({ name, count }))
  )
})

// === Filtrage dynamique des projets ===
const filteredProjects = computed(() => {
  if (selectedCategory.value === 'Tous') return projects.value
  return projects.value.filter(
    (p) => p.category.toLowerCase() === selectedCategory.value.toLowerCase()
  )
})

// === Liste infinie (copie pour effet looping) ===
const infiniteProjects = computed(() => [...filteredProjects.value, ...filteredProjects.value])

// === Calcul de largeur totale d’un cycle ===
function getLoopWidth() {
  const card = scrollContainer.value?.querySelector('.flex-shrink-0')
  if (!card) return 0
  const style = getComputedStyle(scrollContainer.value)
  const gap = parseInt(style.columnGap || style.gap || 32)
  return (card.offsetWidth + gap) * filteredProjects.value.length
}

// === Scroll automatique ===
function startAutoScroll() {
  if (!scrollContainer.value) return
  clearInterval(scrollInterval)

  scrollInterval = setInterval(() => {
    if (isPaused) return

    const loopWidth = getLoopWidth()
    const container = scrollContainer.value

    // Si on atteint la fin, on revient doucement au début
    if (container.scrollLeft >= loopWidth) {
      container.scrollLeft = 0
    } else {
      container.scrollLeft += 1 // vitesse de défilement (tu peux ajuster ici)
    }
  }, 16) // 16ms ≈ 60fps
}

// === Pause & reprise ===
function pauseScroll() {
  isPaused = true
}
function resumeScroll() {
  isPaused = false
}

// === Scroll manuel via boutons ===
function scrollNext() {
  pauseScroll()
  scrollContainer.value.scrollBy({ left: 400, behavior: 'smooth' })
  setTimeout(resumeScroll, 800)
}
function scrollPrev() {
  pauseScroll()
  scrollContainer.value.scrollBy({ left: -400, behavior: 'smooth' })
  setTimeout(resumeScroll, 800)
}

// === Initialisation ===
onMounted(() => {
  startAutoScroll()
})
onBeforeUnmount(() => clearInterval(scrollInterval))

// === Reset du scroll après changement de catégorie ===
watch(filteredProjects, async () => {
  pauseScroll()
  await nextTick()
  if (scrollContainer.value) scrollContainer.value.scrollLeft = 0
  resumeScroll()
})
</script>

<style scoped>
.scrollbar-hide::-webkit-scrollbar { display: none; }
.scrollbar-hide { -ms-overflow-style: none; scrollbar-width: none; }
</style>
