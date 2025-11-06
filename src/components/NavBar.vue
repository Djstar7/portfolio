<template>
  <header class="flex justify-between items-center p-6 opacity-90 relative z-20 bg-[#111837]">
    <!-- Logo -->
    <div class="text-white text-3xl font-bold">
      <img :src="Logo" class="w-12 h-12"/>
    </div>

    <!-- Mobile toggle button -->
    <div class="md:hidden z-30">
      <button type="button" @click="isMenuOpen = !isMenuOpen" class="block focus:outline-none">
        <span v-if="isMenuOpen" class="text-5xl">
          <i class="fas fa-xmark text-white"></i>
        </span>
        <span v-else class="text-5xl">
          <i class="fas fa-bars text-white"></i>
        </span>
      </button>
    </div>

    <!-- Navbar links -->
    <nav
      :class="[
        isMenuOpen ? 'block' : 'hidden',
        'fixed inset-0 z-20 flex flex-col items-center justify-center bg-[#111837] md:relative md:bg-transparent md:flex md:justify-between md:flex-row'
      ]"
    >
      <ul class="flex flex-col items-center space-y-5 md:flex-row md:space-x-5 md:space-y-0">
        <li v-for="item in Menu" :key="item.name">
          <a
            :href="item.href"
            @click="scrollToSection(item.href)"
            class="block text-white hover:text-amber-500 transition ease-linear text-2xl md:text-lg"
          >
            {{ item.name }}
          </a>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script setup>
import { ref } from 'vue'
import Logo from '../assets/icons/logo.png'

const Menu = ref([
  { name: 'Services', href: '#services' },
  { name: 'À propos de moi', href: '#about' },
  { name: 'Compétences', href: '#skills' },
  { name: 'Projets', href: '#projects' },
  { name: 'Contact', href: '#contact' }
])
const isMenuOpen = ref(false)

const scrollToSection = (href) => {
  isMenuOpen.value = false
  const section = document.querySelector(href)
  if(section){
    section.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>

<style scoped>
/* Optionnel : petite transition pour l'ouverture du menu */
nav {
  transition: all 0.3s ease-in-out;
}
</style>
