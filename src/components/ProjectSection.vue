<template>
    <section class="text-white mt-20 bg-gradient-to-br from-[#1e293b] via-[#111a2e] to-[#0f172a] min-h-screen" id="projects">
        <div class="px-4 xl:pl-16">
            <div class="mb-4 md:flex md:justify-between xl:pr-16">
                <h2 class="text-white font-bold text-4xl drop-shadow-lg">
                    Mes <span class="text-transparent bg-clip-text bg-gradient-to-r from-orange-400 via-pink-500 to-purple-600">Projects recents</span>
                </h2>
                <div class="flex space-x-4 mb-4 mt-5 md:mt-0">
                    <button
                        class="px-4 py-2 sm:px-8 sm:py-4 rounded-lg transition-all duration-200 font-semibold border border-transparent hover:border-orange-400 hover:bg-gradient-to-r hover:from-orange-400 hover:to-pink-500 hover:text-white focus:outline-none"
                        :class="selectedCategory === category ? 'bg-gradient-to-r from-orange-400 to-pink-500 text-white shadow-lg' : 'bg-[#1e293b] text-gray-300'"
                        v-for="category in ['Tous', 'Developpement Web', 'Developpement Mobile']"
                        :key="category"
                        @click="selectedCategory = category"
                    >
                        {{ category }}
                    </button>
                </div>
            </div>
            <ul class="grid grid-cols-1 gap-8 mx-4 mt-10 sm:py-16 xl:pr-16 sm:grid-cols-2 md:gap-12 md:pt-12 lg:grid-cols-3" data-aos="fade-right">
                <div v-for="project in filteredProjects" :key="project.id">
                    <div class="h-52 md:h-[24rem] rounded-t-xl relative group shadow-xl transition-transform duration-300 hover:scale-105"
                        :style="{backgroundImage: 'url('+project.image+')', backgroundSize: 'cover', backgroundPosition: 'center',backgroundRepeat: 'no-repeat'}">
                        <div class="overlay items-center justify-center absolute top-0 left-0 w-full h-full bg-gradient-to-br from-blue-900/80 to-pink-900/70 opacity-0 group-hover:opacity-100 flex backdrop-blur-sm transition-all duration-500">
                            <a
                                class="w-14 h-14 mx-2 border-2 relative rounded-full border-orange-400 hover:border-white bg-white/10 flex items-center justify-center transition-all duration-200"
                                :href="project.webURL"
                                target="_blank"
                                v-if="project.webURL"
                            >
                                <svg xmlns="http://www.w3.org/2000/svg" width="28" height="28" fill="none" viewBox="0 0 24 24">
                                    <path fill="currentColor" d="M12 4.5c-5 0-9 4.5-9 7.5s4 7.5 9 7.5 9-4.5 9-7.5-4-7.5-9-7.5zm0 13c-3.87 0-7-3.13-7-5.5S8.13 6.5 12 6.5s7 3.13 7 5.5-3.13 5.5-7 5.5zm0-9A3.5 3.5 0 1 0 12 16a3.5 3.5 0 0 0 0-7zm0 5.5A2 2 0 1 1 12 9a2 2 0 0 1 0 4z"/>
                                </svg>
                            </a>
                            <a
                                class="w-14 h-14 mx-2 border-2 relative rounded-full border-pink-500 hover:border-white bg-white/10 flex items-center justify-center transition-all duration-200"
                                :href="project.gitURL"
                                target="_blank"
                                v-if="project.gitURL"
                            >
                                <svg class="text-2xl" width="28" height="28" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
                                    <path d="M12 2C6.477 2 2 6.484 2 12.021c0 4.428 2.865 8.184 6.839 9.504.5.092.682-.217.682-.483 0-.237-.009-.868-.014-1.703-2.782.605-3.369-1.342-3.369-1.342-.454-1.154-1.11-1.462-1.11-1.462-.908-.62.069-.608.069-.608 1.004.07 1.532 1.032 1.532 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.339-2.221-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.254-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.025A9.564 9.564 0 0 1 12 6.844c.85.004 1.705.115 2.504.337 1.909-1.295 2.748-1.025 2.748-1.025.546 1.378.202 2.396.1 2.65.64.7 1.028 1.595 1.028 2.688 0 3.847-2.337 4.695-4.566 4.944.359.309.678.919.678 1.852 0 1.336-.012 2.415-.012 2.744 0 .268.18.579.688.481C19.138 20.2 22 16.447 22 12.021 22 6.484 17.523 2 12 2z"/>
                                </svg>
                            </a>
                        </div>
                    </div>
                    <div class="text-white rounded-b-xl mt-1 bg-gradient-to-br from-[#1e293b]/90 to-[#111a2e]/90 shadow-2xl border border-[#312e81] py-6 px-4">
                        <h3 class="text-lg font-semibold uppercase lg:text-xl text-orange-400 drop-shadow">
                            {{ project.name }}
                        </h3>
                        <p class="text-[#f3f4f6] mt-2">
                            {{ project.description }}
                        </p>
                        <div class="flex flex-wrap gap-2.5 mt-4">
                            <div
                                v-for="technology in project.technologie"
                                :key="technology"
                                class="text-center text-xs px-4 py-2 rounded-xl bg-gradient-to-r from-pink-500/80 to-orange-400/80 text-white font-semibold shadow"
                                style="border: 1px solid #f472b6; backdrop-filter: blur(6px);"
                            >
                                {{ technology }}
                            </div>
                        </div>
                    </div>
                </div>    
            </ul>
        </div>
    </section>
</template>

<script setup>
import { ref, computed } from 'vue';

import VueImage from '../assets/image1Construction.png'
import LogoImage from '../assets/logo.png'
import DevelopmentImage from '../assets/development.webp'

const projects = ref([
    {
        id: 1,
        category: 'Developpement Web',
        name: 'Civil Design',
        image: VueImage,
        description: 'Un site qui propose les cours de formations en logiciles  AutoDesk ainsi que les plan de maisons',
        technologie: ['Laravel 12', 'Vue JS 3', 'TailwindCSS'],
        gitURL: 'https://github.com/Djstar7/Site-de-formation-autodesk/',
        webURL: '../../../Site Form-Plans/assets/civil.mp4'
    },
    {
        id: 2,
        category: 'Developpement Web',
        name: 'Epreuves-Examens',
        image: LogoImage,
        description: 'Un site qui propose les anciens sujets d\'examens dans tous les niveaux d\'enseignements',
        technologie: ['Laravel 12', 'Vue JS 3', 'TailwindCSS'],
        gitURL: 'https://github.com/Djstar7/epreuves-examens.git',
        webURL: '../../Site Form-Plans/assets/epreuve.mp4'
    },
    {
        id: 3,
        category: 'Developpement Web',
        name: 'DevPerso',
        image: DevelopmentImage,
        description: 'Un site qui propose les cours de developpement personnel',
        technologie: ['PHP & SQL', 'JavaScript', 'Bootstrap'],
        gitURL: 'https://github.com/Djstar7/biblio',
        webURL: ''
    },
])

const selectedCategory = ref('Tous')
const filteredProjects = computed(() => {
    if(selectedCategory.value.toLowerCase() === 'tous'){
        return projects.value
    }
    return projects.value.filter(project =>
        project.category.toLowerCase() === selectedCategory.value.toLowerCase()
    )
})
</script>


















