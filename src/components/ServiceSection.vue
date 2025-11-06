<template>
  <section class="text-white mt-20" id="services">
    <div class="px-4 xl:px-16 text-center xl:text-left">
      <h2 class="text-4xl font-bold mb-10">Mes Services Spécialisés</h2>
    </div>

    <div class="grid gap-8 px-4 xl:px-16 sm:grid-cols-1 md:grid-cols-2 lg:grid-cols-3">
      <!-- Service 1 -->
      <div
        class="bg-[#111a3c] p-6 rounded-2xl shadow-xl hover:scale-[1.02] transition-transform duration-300"
        data-aos="fade-up"
      >
        <div class="flex justify-center mb-5">
          <img
            src="../assets/development-web.svg"
            alt="Développement Web Full-Stack"
            class="w-16 h-16 xl:w-20 xl:h-20 object-contain"
          />
        </div>
        <h3 class="text-2xl font-semibold text-center mb-3 text-transparent bg-clip-text bg-gradient-to-r from-amber-500 to-pink-500">
          Développement Web Full-Stack
        </h3>
        <p class="text-gray-300 text-center text-base hover:text-white transition duration-300">
          Création d'applications web complètes avec Laravel (backend) et Vue.js/JavaScript (frontend). Architecture MVC, API REST, sécurité, et performance optimale. Intégration paiement (CinetPay/NotchPay), authentification avancée, et bases de données SQL optimisées.
        </p>
      </div>

      <!-- Service 2 -->
      <div
        class="bg-[#111a3c] p-6 rounded-2xl shadow-xl hover:scale-[1.02] transition-transform duration-300"
        data-aos="fade-up"
      >
        <div class="flex justify-center mb-5">
          <img
            src="../assets/mobile-development.svg"
            alt="Applications Mobiles"
            class="w-16 h-16 xl:w-20 xl:h-20 object-contain filter brightness-0 invert"
          />
        </div>
        <h3 class="text-2xl font-semibold text-center mb-3 text-transparent bg-clip-text bg-gradient-to-r from-amber-500 to-pink-500">
          Applications Mobiles
        </h3>
        <p class="text-gray-300 text-center text-base hover:text-white transition duration-300">
          Développement d'applications mobiles multiplateformes avec Flutter et Dart. Architecture modulaire, gestion d'état, intégration API, et connexion à backend Laravel. Applications natives performantes pour Android et iOS avec une expérience utilisateur fluide.
        </p>
      </div>

      <!-- Service 3 -->
      <div
        class="bg-[#111a3c] p-6 rounded-2xl shadow-xl hover:scale-[1.02] transition-transform duration-300"
        data-aos="fade-up"
      >
        <div class="flex justify-center mb-5">
          <img
            src="../assets/web-development.svg"
            alt="Architecture et Sécurité Web"
            class="w-16 h-16 xl:w-20 xl:h-20 object-contain filter brightness-0 invert"
          />
        </div>
        <h3 class="text-2xl font-semibold text-center mb-3 text-transparent bg-clip-text bg-gradient-to-r from-amber-500 to-pink-500">
          Architecture & Sécurité Web
        </h3>
        <p class="text-gray-300 text-center text-base hover:text-white transition duration-300">
          Conception d'architectures logicielles robustes, sécurisation des applications web, optimisation des performances et intégration API. Expertise en Laravel (MVC, Eloquent, Authentification), sécurité (UUID, tokens), et bonnes pratiques de développement orienté objet.
        </p>
      </div>
    </div>
  </section>
</template>

<script setup>
import AOS from 'aos'
import 'aos/dist/aos.css'
AOS.init()
</script>

<style scoped>
/* Ajoute tes styles personnalisés ici si besoin */
</style>