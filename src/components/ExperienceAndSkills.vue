<template>
    <section class="text-white mt-10" id="skills">
        <!-- Effets de fond -->
        <div class="absolute right-0 top-[110rem] w-full h-full justify-end z-0">
            <span class="flex opacity-20">
                <span class="h-16 w-32 rounded-l-full bg-amber-500 blur-2xl"></span>
                <span class="h-16 w-32 rounded-r-full bg-pink-300 blur-2xl"></span>
            </span>
        </div>

        <!-- Contenu principal -->
        <div class="relative md:grid md:grid-cols-2 gap-8 items-center py-8 px-4 xl:gap-16 xl:px-16 z-10">

            <!-- Langages -->
            <div class="text-left flex flex-col w-full">
                <h2 class="text-4xl font-bold mb-4">
                    Mes
                    <span class="text-transparent bg-clip-text bg-gradient-to-r from-amber-500 to-pink-500">Langages maîtrisés</span>
                </h2>
                <div
                    v-for="skill in skills"
                    :key="skill.id"
                    class="mt-6"
                    data-aos="fade-right"
                >
                    <div class="flex items-center justify-between">
                        <div class="flex items-center gap-2">
                            <span v-html="skill.icon" class="w-6 h-6"></span>
                            <h4 class="font-semibold">{{ skill.name }}</h4>
                        </div>
                        <h3 class="font-bold text-2xl">{{ skill.width }}</h3>
                    </div>
                    <div class="w-full h-2 mt-2 bg-[#02062b] rounded-full">
                        <div
                            class="h-2 rounded-full"
                            :style="`width: ${skill.width}; background: ${skill.color}`"
                        ></div>
                    </div>
                </div>
            </div>

            <!-- Frameworks -->
            <div class="text-left flex flex-col w-full">
                <h2 class="text-4xl font-bold mb-4">
                    Mes
                    <span class="text-transparent bg-clip-text bg-gradient-to-r from-amber-500 to-pink-500">Technologies</span>
                </h2>
                <div
                    v-for="tech in techs"
                    :key="tech.id"
                    class="mt-6"
                    data-aos="fade-left"
                >
                    <div class="flex items-center justify-between">
                        <div class="flex items-center gap-2">
                            <span v-html="tech.icon" class="w-6 h-6"></span>
                            <h4 class="font-semibold">{{ tech.name }}</h4>
                        </div>
                        <h3 class="font-bold text-2xl">{{ tech.width }}</h3>
                    </div>
                    <div class="w-full h-2 mt-2 bg-[#02062b] rounded-full">
                        <div
                            class="h-2 rounded-full"
                            :style="`width: ${tech.width}; background: ${tech.color}`"
                        ></div>
                    </div>
                </div>
            </div>

        </div>
    </section>
</template>

<script setup>
import { ref } from 'vue'

const skills = ref([
    {
        id: 1,
        name: 'HTML & CSS',
        width: '80%',
        color: 'linear-gradient(to right, #e44d26, #264de4)',
        icon: `
            <span style="display: flex; gap: 2px;">
            <svg xmlns="http://www.w3.org/2000/svg" fill="#e34f26" width="20" height="20" viewBox="0 0 24 24"><path d="M1.5 0h21l-1.91 21.6L12 24l-8.59-2.4z"/><path d="M12 22l7.16-1.93L20.5 2h-17l1.34 18.07z" fill="#fff"/><path d="M12 17.2l-3.18-.9-.2-2h3.38v-2.8H8.5l-.13-1.5h3.63V7.5H6.5l.37 4h3.13v2.8H7.5l.13 1.5h4.37v2.4zm0 0l3.18-.9.2-2h-3.38v-2.8h3.63l.13-1.5h-3.76V7.5h5.5l-.37 4h-3.13v2.8h3.5l-.13 1.5h-4.37v2.4z" fill="#ebebeb"/></svg>
            <svg xmlns="http://www.w3.org/2000/svg" fill="#264de4" width="20" height="20" viewBox="0 0 24 24"><path d="M1.5 0h21l-1.91 21.6L12 24l-8.59-2.4z"/><path d="M12 22l7.16-1.93L20.5 2h-17l1.34 18.07z" fill="#fff"/><path d="M12 11.5v2.9l-3.18-.9-.2-2h3.38z" fill="#ebebeb"/><path d="M12 4h8.5l-.37 4H12z" fill="#fff"/></svg>
            </span>
        `
        },
    {
        id: 2,
        name: 'JavaScript',
        width: '79%',
        color: 'linear-gradient(to right, #f7df1e, #ffe900)',
        icon: `<svg xmlns="http://www.w3.org/2000/svg" fill="#f7df1e" viewBox="0 0 24 24"><path d="M2 2v20h20V2H2zm11.48 17.3c0 1.8-1.05 2.64-2.6 2.64-1.4 0-2.18-.73-2.6-1.6l1.36-.82c.26.45.5.83 1.08.83.55 0 .9-.21.9-1.03v-5.6h1.86v5.58zm5.2 2.6c-1.6 0-2.63-.76-3.14-1.76l1.36-.8c.36.6.83 1.05 1.63 1.05.69 0 1.13-.35 1.13-.84 0-.58-.45-.78-1.2-1.12l-.42-.18c-1.22-.52-2.03-1.18-2.03-2.58 0-1.29.98-2.27 2.52-2.27 1.1 0 1.89.38 2.47 1.38l-1.33.86c-.29-.52-.6-.72-1.14-.72-.52 0-.84.32-.84.72 0 .5.32.7 1.07 1.02l.42.18c1.42.6 2.23 1.24 2.23 2.7-.01 1.55-1.22 2.4-2.84 2.4z"/></svg>`
    },
    {
        id: 3,
        name: 'PHP & SQL',
        width: '60%',
        color: 'linear-gradient(to right, #8892be, #4f5b93)',
        icon: `<svg xmlns="http://www.w3.org/2000/svg" fill="#8892be" viewBox="0 0 24 24"><path d="M12 0C5.4 0 0 3.6 0 8v8c0 4.4 5.4 8 12 8s12-3.6 12-8V8c0-4.4-5.4-8-12-8zm0 22c-5.5 0-10-2.7-10-6v-1.2c2.2 1.8 5.9 3.2 10 3.2s7.8-1.4 10-3.2V16c0 3.3-4.5 6-10 6zm0-5c-5.5 0-10-2.7-10-6s4.5-6 10-6 10 2.7 10 6-4.5 6-10 6z"/></svg>`
    },
    {
        id: 4,
        name: 'TypeScript',
        width: '40%',
        color: 'linear-gradient(to right, #3178c6, #61dafb)',
        icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 32 32" width="20" height="20"><rect width="32" height="32" rx="6" fill="#3178C6"/><path d="M13.44 14.56v1.36h-3.36v8.08h-1.76v-8.08H5v-1.36h8.44zm6.32 9.44c-.8 0-1.56-.16-2.16-.48-.6-.32-1.12-.8-1.44-1.36l1.36-.8c.24.4.52.72.88.92.36.2.76.32 1.24.32.52 0 .92-.12 1.2-.36.28-.24.44-.56.44-.96 0-.32-.12-.56-.36-.76-.24-.2-.68-.4-1.32-.6-.96-.32-1.64-.68-2.04-1.08-.4-.4-.6-.92-.6-1.56 0-.56.16-1.04.48-1.44.32-.4.76-.72 1.32-.92.56-.2 1.2-.32 1.92-.32.72 0 1.36.12 1.92.36.56.24 1 .6 1.32 1.08l-1.28.88c-.2-.28-.44-.48-.72-.6-.28-.12-.6-.2-.96-.2-.48 0-.84.1-1.08.3-.24.2-.36.46-.36.78 0 .28.12.5.36.68.24.18.7.38 1.38.6.92.3 1.58.66 1.98 1.08.4.42.6.96.6 1.62 0 .56-.16 1.06-.48 1.48-.32.42-.76.74-1.32.96-.56.22-1.2.34-1.92.34z" fill="#fff"/></svg>`
    },
    {
        id: 5,
        name: 'Python',
        width: '15%',
        color: 'linear-gradient(to right, #3776ab, #ffd343)',
        icon: `
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 256 255" width="40" height="40">
            <defs>
                <linearGradient id="a" x1="12.959%" x2="79.639%" y1="12.039%" y2="78.201%">
                <stop offset="0%" stop-color="#387EB8"/>
                <stop offset="100%" stop-color="#366994"/>
                </linearGradient>
                <linearGradient id="b" x1="19.128%" x2="90.742%" y1="20.579%" y2="88.429%">
                <stop offset="0%" stop-color="#FFE052"/>
                <stop offset="100%" stop-color="#FFC331"/>
                </linearGradient>
            </defs>
            <path fill="url(#a)" d="M126.916.007c-10.708.047-20.932.978-29.957 2.623C81.3 5.37 76.165 8.253 76.165 16.03v20.364h51.502v6.788H76.165 53.332c-8.108 0-15.243 4.89-17.464 15.37-2.566 12.144-2.68 19.703 0 32.49 1.98 9.523 6.715 15.37 14.823 15.37h18.804v-24.96c0-10.122 8.38-18.75 18.825-18.75h51.45c8.35 0 15.18-6.914 15.18-15.274V16.03c0-8.104-6.867-13.508-15.18-15.4-10.404-2.314-21.11-2.65-31.033-2.623zM98.565 20.57c4.624 0 8.383 3.786 8.383 8.445 0 4.65-3.76 8.41-8.383 8.41-4.625 0-8.384-3.76-8.384-8.41 0-4.66 3.76-8.446 8.384-8.446z"/>
            <path fill="url(#b)" d="M180.973 45.218v22.98c0 10.33-8.74 18.824-18.826 18.824h-51.45c-8.303 0-15.18 6.922-15.18 15.274v43.424c0 8.106 7.056 12.872 15.18 15.274 9.6 2.807 18.778 3.306 29.957 0 7.52-2.178 15.18-6.564 15.18-15.274v-20.34h-51.45v-6.788h51.45 25.726c8.108 0 11.13-6.53 13.356-15.37 2.787-11.59 2.67-22.72 0-32.49-2.007-7.27-5.223-15.37-13.356-15.37h-18.825zm-27.214 115.46c4.625 0 8.384 3.76 8.384 8.41 0 4.66-3.76 8.445-8.384 8.445-4.624 0-8.383-3.786-8.383-8.445 0-4.65 3.76-8.41 8.383-8.41z"/>
            </svg>
        `
   },
    {
        id: 6,
        name: 'Langage C',
        width: '30%',
        color: 'linear-gradient(to right, #00599c, #007acc)',
        icon: `<svg xmlns="http://www.w3.org/2000/svg" fill="#00599c" viewBox="0 0 24 24"><path d="M12 0L1 6v12l11 6 11-6V6L12 0zm0 1.8l9.2 5.2v10L12 22.2 2.8 17V7L12 1.8zm1 4.7c-2.8 0-5 2.2-5 5s2.2 5 5 5c1.8 0 3.3-.9 4.3-2.2l-1.5-1c-.6.9-1.6 1.5-2.8 1.5-1.9 0-3.3-1.5-3.3-3.3 0-1.9 1.5-3.3 3.3-3.3 1.2 0 2.2.6 2.8 1.5l1.5-1C16.3 7.4 14.8 6.5 13 6.5z"/></svg>`
    }
])

const techs = ref([
    {
        id: 1,
        name: 'TailwindCSS',
        width: '90%',
        color: 'linear-gradient(to right, #38bdf8, #0ea5e9)',
        icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 48" width="20" height="20"><g><path fill="#38bdf8" d="M24 14c-5.333 0-8.667 2.667-10 8 2-2.667 4.333-3.667 7-3 1.533.383 2.633 1.483 3.7 2.55C26.767 23.617 27.867 24.717 29.4 25.1c2.667.667 5-1.333 7-4-1.333-5.333-4.667-8-10-8zm-10 10c-5.333 0-8.667 2.667-10 8 2-2.667 4.333-3.667 7-3 1.533.383 2.633 1.483 3.7 2.55C16.767 35.617 17.867 36.717 19.4 37.1c2.667.667 5-1.333 7-4-1.333-5.333-4.667-8-10-8z"/></g></svg>`
    },
    {
        id: 2,
        name: 'Vue JS',
        width: '75%',
        color: 'linear-gradient(to right, #42b883, #35495e)',
        icon: `<svg xmlns="http://www.w3.org/2000/svg" fill="#42b883" viewBox="0 0 24 24"><path d="M2 3h4l6 10 6-10h4l-10 17L2 3z"/></svg>`
    },
    {
        id: 3,
        name: 'Laravel',
        width: '60%',
        color: 'linear-gradient(to right, #ff2d20, #ff7c68)',
        icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 256 256" width="20" height="20"><g fill="none"><path d="M16.7 61.2a13.3 13.3 0 0 1 6.6-11.5l44.6-25.7a13.3 13.3 0 0 1 13.3 0l44.6 25.7a13.3 13.3 0 0 1 6.6 11.5v51.4a13.3 13.3 0 0 1-6.6 11.5l-44.6 25.7a13.3 13.3 0 0 1-13.3 0l-44.6-25.7a13.3 13.3 0 0 1-6.6-11.5V61.2zm122.8 0a13.3 13.3 0 0 1 6.6-11.5l44.6-25.7a13.3 13.3 0 0 1 13.3 0l44.6 25.7a13.3 13.3 0 0 1 6.6 11.5v51.4a13.3 13.3 0 0 1-6.6 11.5l-44.6 25.7a13.3 13.3 0 0 1-13.3 0l-44.6-25.7a13.3 13.3 0 0 1-6.6-11.5V61.2zm-61.4 92.2a13.3 13.3 0 0 1 13.3 0l44.6 25.7a13.3 13.3 0 0 1 6.6 11.5v51.4a13.3 13.3 0 0 1-6.6 11.5l-44.6 25.7a13.3 13.3 0 0 1-13.3 0l-44.6-25.7a13.3 13.3 0 0 1-6.6-11.5v-51.4a13.3 13.3 0 0 1 6.6-11.5l44.6-25.7zm122.8 0a13.3 13.3 0 0 1 13.3 0l44.6 25.7a13.3 13.3 0 0 1 6.6 11.5v51.4a13.3 13.3 0 0 1-6.6 11.5l-44.6 25.7a13.3 13.3 0 0 1-13.3 0l-44.6-25.7a13.3 13.3 0 0 1-6.6-11.5v-51.4a13.3 13.3 0 0 1 6.6-11.5l44.6-25.7z" fill="#ff2d20"/></g></svg>`
    },
    {
        id: 4,
        name: 'React JS',
        width: '35%',
        color: 'linear-gradient(to right, #61dafb, #1f2937)',
        icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 32 32" width="20" height="20"><g><circle cx="16" cy="16" r="2.5" fill="#61dafb"/><g stroke="#61dafb" stroke-width="2" fill="none"><ellipse rx="11" ry="4.2" cx="16" cy="16" transform="rotate(60 16 16)"/><ellipse rx="11" ry="4.2" cx="16" cy="16" transform="rotate(120 16 16)"/><ellipse rx="11" ry="4.2" cx="16" cy="16"/></g></g></svg>`
    }
])
</script>
