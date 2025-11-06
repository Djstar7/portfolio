<template>
  <div
    class="rounded-xl shadow-2xl overflow-hidden relative transition-transform duration-300 hover:scale-105 flex-shrink-0 group w-full flex flex-col h-full"
  >
    <!-- Conteneur pour l'image avec un ratio d'aspect fixe -->
    <div
      class="w-full relative overflow-hidden"
      style="padding-top: 56.25%;" 
    >
      <div
        class="absolute inset-0 bg-cover bg-center"
        :style="{ backgroundImage: 'url(' + project.image + ')' }"
      >
        <!-- Overlay affiché au hover -->
        <div
          class="absolute inset-0 bg-black/70 flex flex-col justify-center items-center text-center opacity-0 group-hover:opacity-100 transition-all duration-500 backdrop-blur-sm px-3 sm:px-4 py-4"
        >
          <p class="text-gray-100 text-[10px] sm:text-xs md:text-sm lg:text-base leading-relaxed">
            {{ project.description }}
          </p>
        </div>
      </div>
    </div>

    <!-- Infos du projet -->
    <div class="bg-gradient-to-br from-[#1e293b]/90 to-[#111a2e]/90 p-3 sm:p-5 flex flex-col gap-3 h-auto flex-grow">
      <!-- Nom du projet -->
      <h3 class="text-sm sm:text-base md:text-lg lg:text-xl font-semibold uppercase text-orange-400 drop-shadow break-words">
        {{ project.name }}
      </h3>

      <!-- Stack / technologies -->
      <div class="flex flex-wrap gap-2">
        <div
          v-for="tech in project.technologie"
          :key="tech"
          class="text-[9px] sm:text-xs px-2 py-0.5 rounded-xl bg-gradient-to-r from-pink-500/80 to-orange-400/80 text-white font-semibold shadow break-words max-w-full"
          style="border: 1px solid #f472b6; backdrop-filter: blur(6px);"
        >
          {{ tech }}
        </div>
      </div>
    </div>
</div>
</template>

<script setup>
defineProps({
  project: {
    type: Object,
    required: true
  }
});
</script>

<style scoped>
/*
  Le style pour le ratio d'aspect est intégré directement via `padding-top` pour une meilleure encapsulation.
  Ceci garantit que l'image a toujours une hauteur proportionnelle à sa largeur.
*/
</style>