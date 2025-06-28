<template>
  <div class="bg-[#111837] min-h-screen">
    <NavBar/>
    <HeroSection />
    <ServiceSection />
    <AboutSection />
    <ExperienceAndSkills />
    <ProjectSection />
    <ContactSection />
  </div>
</template>
<script setup>
import { defineAsyncComponent } from 'vue'
//import components Asynchronoulys
const NavBar = defineAsyncComponent(() => import('./components/NavBar.vue'))
const HeroSection = defineAsyncComponent(() => import('./components/HeroSection.vue'))
const ServiceSection = defineAsyncComponent(() => import('./components/ServiceSection.vue'))
const AboutSection = defineAsyncComponent(() => import('./components/AboutSection.vue'))
const ExperienceAndSkills = defineAsyncComponent(() => import('./components/ExperienceAndSkills.vue'))
const ProjectSection = defineAsyncComponent(() => import('./components/ProjectSection.vue'))
const ContactSection = defineAsyncComponent(() => import('./components/ContactSection.vue'))
</script>