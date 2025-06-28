<template>
    <section class="relative w-full" data-aos="zoom-in-up">
        <!-- Background gradient deco -->
        <div class="absolute top-0 inset-x-0 h-64 flex items-start">
            <div class="h-24 w-2/3 bg-gradient-to-br from-[#570cac] blur-2xl invisible opacity-40"></div>
            <div class="h-20 w-3/5 bg-gradient-to-r from-[#670ccf] opacity-40 blur-2xl"></div>
        </div>

        <!-- Content container -->
        <div class="w-full px-5 sm:px-0 max-w-screen-lg mx-auto relative">
            <div class="grid lg:grid-cols-2 gap-6 xl:gap-14 relative pt-24 items-center">
                <!-- Text block -->
                <div class="lg:py-6">
                    <div class="text-center lg:text-left">
                        <h1 class="pt-4 text-white font-bold text-4xl md:text-5xl lg:text-6xl">
                            Salut, moi c'est
                            <span class="text-transparent bg-clip-text bg-gradient-to-r from-orange-400 to-pink-500">
                                Stael DJUNE  
                            </span>😄
                        </h1>
                        <p class="text-gray-300 pt-8 text-center lg:text-left mx-auto max-w-xl">
                            Je suis un développeur full-stack passionné par la création de solutions web et mobiles modernes.
                            Spécialisé en JavaScript, Laravel, Vue.js et Flutter, j'aime transformer des idées en interfaces fluides
                            et dynamiques. Bienvenue sur mon portfolio !
                        </p>

                        <!-- Buttons -->
                        <div class="flex items-center gap-3 pt-9 flex-col sm:flex-row sm:w-max sm:mx-auto lg:mx-0">
                            <!-- Download CV button -->
                            <a
                                :href="cvPdf"
                                download="Stael_DJUNE_CV.pdf"
                                class="bg-amber-500 hover:bg-amber-600 px-6 md:px-7 py-3 rounded-full flex items-center gap-2 text-white transition-all"
                            >
                                <svg
                                    xmlns="http://www.w3.org/2000/svg"
                                    fill="none"
                                    viewBox="0 0 24 24"
                                    stroke-width="1.5"
                                    stroke="currentColor"
                                    class="w-6 h-6"
                                >
                                    <path
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        d="M4.5 20.25h15m-7.5-15v10.5m0 0l-3-3m3 3l3-3"
                                    />
                                </svg>
                                Télécharger mon CV
                            </a>
                        </div>
                    </div>
                </div>

                <!-- Image block -->
                <div class="flex items-center justify-center">
                    <div class="relative z-20 w-72 h-72 p-2 rounded-full shadow-lg border border-amber-500">
                        <img
                            src="../assets/top_picture.jpg"
                            alt="Photo de Stael DJUNE"
                            class="w-full h-full rounded-full object-cover"
                        />
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref } from 'vue'
import AOS from 'aos'
import 'aos/dist/aos.css'
AOS.init()

// ✅ Import correct d'un PDF dans Vite
import cvPdf from '../assets/CV/moncv.pdf'
</script>

<style scoped>
/* Ajoute ici tes styles si tu veux */
</style>
