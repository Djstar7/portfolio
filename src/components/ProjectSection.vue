<template>
  <section class="text-white mt-20 bg-gradient-to-br from-[#1e293b] via-[#111a2e] to-[#0f172a]" id="projects">
    <div class="px-4 xl:pl-16">
      <!-- Header : Gère le titre et les catégories. Flexbox et classes responsives (md:flex-row) ajustent la disposition sur différents écrans. -->
      <div class="mb-4 flex flex-col md:flex-row md:justify-between md:items-center xl:pr-16">
        <h2 class="text-white font-bold text-4xl drop-shadow-lg mb-4 md:mb-0">
          Mes <span class="text-transparent bg-clip-text bg-gradient-to-r from-orange-400 via-pink-500 to-purple-600">Projets professionnels</span>
        </h2>

        <!-- Categories : Les boutons de catégorie s'ajustent avec flex-wrap pour s'afficher sur plusieurs lignes si l'espace est insuffisant sur les petits écrans. -->
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

      <!-- Scrollable Projects : Conteneur principal du carrousel. Utilise flex pour les cartes et overflow-x-auto pour le défilement. -->
      <div class="relative mt-10 flex items-center">
        <!-- Bouton gauche : Positionné absolument. md:-left-12 le déplace à l'extérieur du conteneur sur les écrans moyens et grands. -->
        <button
          @click="scrollPrev"
          class="absolute left-0 md:-left-12 z-20 bg-gradient-to-r from-orange-500 to-pink-500 text-white text-2xl w-10 h-10 md:w-12 md:h-12 flex justify-center items-center rounded-full shadow-lg hover:scale-110 transition-all duration-300"
        >
          <i class="fas fa-chevron-left"></i>
        </button>

        <!-- Conteneur de défilement des cartes :
             - `flex gap-4 sm:gap-4`: Gère l'espacement entre les cartes.
             - `overflow-x-auto`: Permet le défilement horizontal lorsque le contenu dépasse.
             - `scrollbar-hide`: Masque les barres de défilement (voir CSS en bas).
             - `w-full`: Prend toute la largeur disponible.
             - `px-2 sm:px-4 md:px-6`: Ajoute un padding horizontal responsif pour les bords.
          -->
        <div
          ref="scrollContainer"
          class="flex gap-4 sm:gap-4 overflow-x-auto scroll-smooth scrollbar-hide px-2 sm:px-4 md:px-6 py-4 w-full"
          @mouseenter="pauseScroll"
          @mouseleave="resumeScroll"
        >
          <!-- Carte de projet :
               - `flex-shrink-0`: Empêche les cartes de se réduire pour tenir dans le conteneur.
               - `w-[180px] sm:w-[220px] md:w-[300px] lg:w-[350px] xl:w-[400px]`: Définit des largeurs de carte responsives,
                 permettant aux cartes de s'agrandir sur des écrans plus grands tout en conservant leur taille sur les petits.
               - `h-[320px] md:h-[350px] lg:h-[380px] xl:h-[400px]`: Hauteurs responsives pour maintenir la proportion.
          -->
          <div
            v-for="(project, idx) in infiniteProjects"
            :key="project.id + '-' + idx"
            class="flex-shrink-0 w-[180px] sm:w-[220px] md:w-[300px] lg:w-[350px] xl:w-[400px] h-[320px] md:h-[350px] lg:h-[380px] xl:h-[400px] bg-[#1f2937] rounded-xl shadow-lg p-4 hover:scale-105 transition-transform duration-300 flex flex-col justify-between"
          >
            <ProjectCard :project="project" />
          </div>
        </div>

        <!-- Bouton droit : Identique au bouton gauche, positionné à droite. -->
        <button
          @click="scrollNext"
          class="absolute right-0 md:-right-12 z-20 bg-gradient-to-r from-orange-500 to-pink-500 text-white text-2xl w-10 h-10 md:w-12 md:h-12 flex justify-center items-center rounded-full shadow-lg hover:scale-110 transition-all duration-300"
        >
          <i class="fas fa-chevron-right"></i>
        </button>
      </div>
    </div>
  </section>
</template>

// --- SCRIPT SETUP CORRIGÉ ---
<script setup>
import { ref, computed, onMounted, onBeforeUnmount, watch, nextTick } from 'vue'
import ProjectCard from './ProjectCard.vue'
import VueImage from '../assets/icons/cd.png'
import EE from '../assets/ee.png'
import Sie from '../assets/icons/sie.png'
import logoImage from '../assets/icons/logo.png'
import DevelopmentImage from '../assets/development.webp'

// === Projets ===
const projects = ref([
  { id: 1, category: 'Développement Web', name: 'Civil Design', image: VueImage, description: 'Civil Design est une plateforme complète permettant la vente de plans de maisons ainsi que des formations aux logiciels Autodesk.', technologie: ['Laravel','Vue.js 3','TypeScript','TailwindCSS','MySQL'] },
  { id: 2, category: 'Développement Web', name: 'SIE', image: Sie, description: 'Plateforme permettant de gérer les procédures d\'obtention de visa.', technologie: ['Laravel','Vue.js 3','TypeScript','TailwindCSS','MySQL'] },
  { id: 3, category: 'Développement Web', name: 'Site Epreuves-Examens', image: EE, description: 'Plateforme pour accéder et acheter les épreuves des examens officiels passés.', technologie: ['Laravel','Vue.js 3','TypeScript','TailwindCSS','MySQL'] },
  { id: 4, category: 'Développement Web', name: 'Site DevPerso', image: DevelopmentImage, description: 'Bibliothèque en ligne avec vente de livres et gestion des utilisateurs. CRUD complet sur livres et utilisateurs, paiement simple et interface intuitive.', technologie: ['PHP POO','MySQL','HTML','CSS','Bootstrap'] },
  { id: 5, category: 'Outils Web', name: 'Mini Calco', image: logoImage, description: 'Application web pour effectuer des calculs complexes avec interface fluide.', technologie: ['HTML','CSS','JavaScript'] },
  { id: 6, category: 'IA/Full-Stack', name: 'Mini Chatbot AI', image: logoImage, description: 'Chatbot intelligent répondant aux questions des utilisateurs en temps réel.', technologie: ['NestJS','React JS','JavaScript'] },
  { id: 7, category: 'Outils Web', name: 'Mini Calendar', image: logoImage, description: 'Fournit le calendrier exact pour un nombre de mois précis. Gère les décalages, années bissextiles et affichage clair.', technologie: ['HTML','CSS','JavaScript'] }
])

const selectedCategory = ref('Tous')
const scrollContainer = ref(null)
let scrollInterval = null
let isPaused = false

// === Catégories dynamiques ===
const categories = computed(() => {
  const map = projects.value.reduce((acc, p) => {
    acc[p.category] = (acc[p.category] || 0) + 1
    return acc
  }, {})
  return [{ name: 'Tous', count: projects.value.length }].concat(
    Object.entries(map).map(([name, count]) => ({ name, count }))
  )
})

// === Projets filtrés ===
const filteredProjects = computed(() => selectedCategory.value === 'Tous' ? projects.value : projects.value.filter(p => p.category === selectedCategory.value))

// === Infinite projects pour scroll looping ===
const infiniteProjects = computed(() => [...filteredProjects.value, ...filteredProjects.value])

// === Scroll automatique responsive et rapide ===
function startAutoScroll() {
  clearInterval(scrollInterval)
  
  // Correction 1: Assure que scrollContainer existe et que le contenu est présent
  if (!scrollContainer.value || filteredProjects.value.length === 0) {
      return;
  }
  
  // Correction : Recalcule la halfWidth à chaque appel pour gérer le redimensionnement
  const halfWidth = scrollContainer.value.scrollWidth / 2 
  
  scrollInterval = setInterval(() => {
    if (!isPaused && scrollContainer.value) {
      const step = 2
      // L'opérateur modulo assure le bouclage
      scrollContainer.value.scrollLeft = (scrollContainer.value.scrollLeft + step) % halfWidth
    }
  }, 48)
}

// === Pause & reprise du défilement automatique ===
function pauseScroll() { isPaused = true }
function resumeScroll() { isPaused = false }

// === Scroll manuel responsive (avec les boutons) ===
function getScrollStep() {
  if (!scrollContainer.value) return 300
  // S'assurer qu'il y a des cartes à l'intérieur
  const card = scrollContainer.value.querySelector('.flex-shrink-0')
  return card ? card.offsetWidth + 16 : 300 // 16px correspond au `gap-4`
}
function scrollNext() {
  pauseScroll() 
  scrollContainer.value.scrollBy({ left: getScrollStep(), behavior: 'smooth' })
  setTimeout(resumeScroll, 600)
}
function scrollPrev() {
  pauseScroll()
  scrollContainer.value.scrollBy({ left: -getScrollStep(), behavior: 'smooth' })
  setTimeout(resumeScroll, 600)
}

// === Cycle de vie du composant (avec correction du redimensionnement) ===
function handleResize() {
  // Redémarre l'intervalle pour recalculer la halfWidth et s'adapter au redimensionnement
  startAutoScroll();
}

onMounted(() => {
  startAutoScroll()
  window.addEventListener('resize', handleResize); // Ajout du gestionnaire de redimensionnement
})
onBeforeUnmount(() => {
  clearInterval(scrollInterval)
  window.removeEventListener('resize', handleResize); // Nettoyage
})

// === Watch (avec correction de la logique de redémarrage) ===
watch(filteredProjects, async () => {
  // 1. Assure que la pause est levée
  isPaused = false; 
  // 2. Attend que le DOM soit mis à jour avec les nouveaux projets filtrés
  await nextTick() 
  // 3. Réinitialise la position de défilement
  if(scrollContainer.value) scrollContainer.value.scrollLeft = 0 
  // 4. Redémarre l'intervalle (qui recalculera la halfWidth)
  startAutoScroll() 
})
</script>
<style scoped>
/* Masque les barres de défilement standard du navigateur pour une esthétique plus propre */
.scrollbar-hide::-webkit-scrollbar { display: none; }
.scrollbar-hide { -ms-overflow-style: none; scrollbar-width: none; }
</style>
