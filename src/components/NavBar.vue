<template>
    <header class="flex justify-between items-center p-6 opacity-50 relative z-20">
        <div class="text-white text-3xl font-bold">LOGO</div>
        <!-- Mobile toggle button -->
        <div class="md:hidden z-30">
            <button type="button" @click="isMenuOpen = !isMenuOpen"  class="block focus:outline-none" >
                <span v-if="isMenuOpen" class="text-5xl">
                    <!-- image button close -->
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="w-6 h-6 text-white"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                        stroke-width="2"
                    >
                    <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                    </svg>

                </span>
                <span v-else class="text-5xl ">
                    <!-- image button menu -->
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="w-6 h-6 text-white"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                        stroke-width="2"
                    >
                    <path stroke-linecap="round" stroke-linejoin="round" d="M4 6h16M4 12h16M4 18h16" />
                    </svg>
                </span>
            </button>
        </div>

        <!-- Navbar link -->
        <nav :class="[isMenuOpen ? 'block': 'hidden','fixed inset-0 z-20 flex flex-col items-center justify-center bg-[#111837] md:relative md:bg-transprent md:flex md:justify-between md:flex-row']">
            <ul class="flex flex-col items-center space-y-5 md:flex-row md:space-x-5 md:space-y-0">
                <li v-for="item in Menu" :key="item.name" >
                    <a :href="item.href" @click="scrollToSection(item.href)" class="block text-white hover:text-amber-500 transition ease-linear text-2xl md:text-lg">{{ item.name }}</a>
                </li>
            </ul>
        </nav>
    </header>
</template>
<script setup>
import { ref } from 'vue'

const Menu = ref([
  { name: 'Services', href: '#services' },
  { name: 'À propos de moi', href: '#about' },
  { name: 'Compétences', href: '#skills' },
  { name: 'Projets', href: '#projects' },
  { name: 'Contact', href: '#contact' }
])
const isMenuOpen = ref(false)

const scrollToSection = (href) => {
    isMenuOpen.value = false;

    const section = document.querySelector(href);
    if(section){
        section.scrollIntoView({ behavior: 'smooth' })
    }
}
</script>