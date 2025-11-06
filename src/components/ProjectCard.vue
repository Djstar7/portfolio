<template>
  <div
    class="w-[350px] lg:w-[400px] rounded-xl shadow-2xl overflow-hidden relative transition-transform duration-300 hover:scale-105 flex-shrink-0 group"
  >
    <!-- Image du projet -->
    <div
      class="h-60 bg-cover bg-center relative"
      :style="{ backgroundImage: 'url(' + project.image + ')' }"
    >
      <!-- Overlay affiché au hover -->
      <div
        class="absolute inset-0 bg-black/70 flex flex-col justify-center items-center text-center opacity-0 group-hover:opacity-100 transition-all duration-500 backdrop-blur-sm px-4"
      >
        <p class="text-gray-100 text-sm leading-relaxed">
          {{ project.description }}
        </p>
      </div>
    </div>

    <!-- Infos du projet -->
    <div class="bg-gradient-to-br from-[#1e293b]/90 to-[#111a2e]/90 p-6 flex flex-col justify-between h-auto max-h-72">
      <div>
        <h3 class="text-lg lg:text-xl font-semibold uppercase text-orange-400 drop-shadow mb-2 break-words">
          {{ project.name }}
        </h3>
      </div>

      <!-- Stack / technologies -->
      <div class="flex flex-wrap gap-2.5 mt-3">
        <div
          v-for="tech in project.technologie"
          :key="tech"
          class="text-xs px-3 py-1 rounded-xl bg-gradient-to-r from-pink-500/80 to-orange-400/80 text-white font-semibold shadow break-words max-w-full"
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
