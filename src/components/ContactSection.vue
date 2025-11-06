<script setup>
import { ref } from 'vue'
import emailjs from '@emailjs/browser'

const formRef = ref(null)
const isLoading = ref(false)
const form = ref({
  user_name: '',
  user_email: '',
  message: ''
})

const successMessage = ref('')
const errorMessage = ref('')

const isValidEmail = (email) => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)

const sendEmail = async () => {
  successMessage.value = ''
  errorMessage.value = ''

  if (!form.value.user_name.trim()) {
    errorMessage.value = 'Le nom est requis.'
    return
  }
  if (!isValidEmail(form.value.user_email)) {
    errorMessage.value = 'Email invalide.'
    return
  }
  if (!form.value.message.trim()) {
    errorMessage.value = 'Le message ne peut pas être vide.'
    return
  }

  isLoading.value = true
  try {
    const response = await emailjs.send(
      'service_m5h88cq',
      'template_3zyhonp',
      {
        from_name: form.value.user_name,
        from_email: form.value.user_email,
        reply_to: form.value.user_email,
        message: form.value.message
      },
      { publicKey: 'nJOj2whyxmE00W8wb' }
    )

    if (response.status === 200) {
      successMessage.value = 'Message envoyé avec succès'
      form.value = { user_name: '', user_email: '', message: '' }
      setTimeout(() => (successMessage.value = ''), 3000)
      formRef.value?.reset()
    } else {
      errorMessage.value = 'Erreur inconnue. Réessaie plus tard.'
    }
  } catch (error) {
    console.error('Erreur EmailJS:', error)
    errorMessage.value = 'Erreur lors de l’envoi. Vérifie ta connexion ou réessaie plus tard.'
  } finally {
    isLoading.value = false
  }
}
</script>

<template>
  <section id="contact" class="py-20 bg-gradient-to-br from-[#0f172a] via-[#111827] to-[#1e293b] text-white overflow-hidden">
    <div class="max-w-7xl mx-auto px-6 md:px-12">
      <div class="text-center mb-16">
        <h2 class="text-4xl md:text-5xl font-extrabold">
          Discutons de votre 
          <span class="text-transparent bg-clip-text bg-gradient-to-r from-orange-400 to-pink-500">Projet</span>
        </h2>
        <p class="text-gray-300 mt-4 text-lg max-w-2xl mx-auto">
          Vous avez une idée de projet web, mobile ou full-stack ?<br />
          Transformons cette idée en une expérience numérique percutante.
        </p>
      </div>

      <div class="grid md:grid-cols-2 gap-10 items-center">
        <!-- Infos Contact -->
        <div class="space-y-8">
          <p class="text-gray-300 leading-relaxed text-lg">
            Collaborons pour donner vie à vos idées. <br>
            Contactez-moi par mail, WhatsApp ou via mes réseaux professionnels.  
            <span class="block mt-3 text-green-500 font-medium">Réponse garantie sous 24h</span>
          </p>

          <div class="space-y-6">
            <div class="flex items-center gap-4">
              <div class="p-3 rounded-xl bg-gradient-to-br from-[#1e293b] to-[#111a2e] shadow-md border border-gray-700">
                <i class="fas fa-envelope text-orange-400 text-xl"></i>
              </div>
              <div>
                <h4 class="text-gray-400 text-sm uppercase">Email</h4>
                <p class="text-white font-medium">infodjstar7@gmail.com</p>
              </div>
            </div>

            <div class="flex items-center gap-4">
              <div class="p-3 rounded-xl bg-gradient-to-br from-[#1e293b] to-[#111a2e] shadow-md border border-gray-700">
                <i class="fab fa-whatsapp text-green-500 text-xl"></i>
              </div>
              <div>
                <h4 class="text-gray-400 text-sm uppercase">WhatsApp</h4>
                <p class="text-white font-medium">+237 6 74 69 36 25</p>
              </div>
            </div>

            <div class="flex items-center gap-4">
              <div class="p-3 rounded-xl bg-gradient-to-br from-[#1e293b] to-[#111a2e] shadow-md border border-gray-700">
                <i class="fab fa-github text-gray-300 text-xl"></i>
              </div>
              <div>
                <h4 class="text-gray-400 text-sm uppercase">GitHub</h4>
                <a href="https://github.com/Djstar7" target="_blank" class="text-blue-400 hover:text-blue-300">
                  github.com/Djstar7
                </a>
              </div>
            </div>

            <div class="flex items-center gap-4">
              <div class="p-3 rounded-xl bg-gradient-to-br from-[#1e293b] to-[#111a2e] shadow-md border border-gray-700">
                <i class="fab fa-linkedin text-blue-500 text-xl"></i>
              </div>
              <div>
                <h4 class="text-gray-400 text-sm uppercase">LinkedIn</h4>
                <a
                  href="https://www.linkedin.com/in/dj-star-info-b34669357/"
                  target="_blank"
                  class="text-blue-400 hover:text-blue-300"
                >
                  linkedin.com/in/dj-star-info-b34669357
                </a>
              </div>
            </div>
          </div>
        </div>

        <!-- Formulaire -->
        <div class="bg-[#1e293b]/60 backdrop-blur-md rounded-2xl shadow-2xl border border-gray-700 p-8">
          <form ref="formRef" @submit.prevent="sendEmail" class="flex flex-col gap-5">
            <input
              v-model="form.user_name"
              type="text"
              name="user_name"
              placeholder="Votre nom complet"
              class="w-full bg-white/10 border border-gray-600 text-white rounded-xl px-4 py-3 focus:ring-2 focus:ring-orange-400 placeholder-gray-400"
            />

            <input
              v-model="form.user_email"
              type="email"
              name="user_email"
              placeholder="Votre adresse email"
              class="w-full bg-white/10 border border-gray-600 text-white rounded-xl px-4 py-3 focus:ring-2 focus:ring-orange-400 placeholder-gray-400"
            />

            <textarea
              v-model="form.message"
              name="message"
              rows="5"
              placeholder="Votre message..."
              class="w-full bg-white/10 border border-gray-600 text-white rounded-xl px-4 py-3 focus:ring-2 focus:ring-orange-400 placeholder-gray-400 resize-none"
            ></textarea>

            <p v-if="successMessage" class="text-green-400 text-center font-medium animate-pulse">{{ successMessage }}</p>
            <p v-if="errorMessage" class="text-red-400 text-center font-medium">{{ errorMessage }}</p>

            <button
              type="submit"
              :disabled="isLoading"
              class="w-full bg-gradient-to-r from-orange-500 to-pink-500 hover:opacity-90 transition-all duration-300 py-3 rounded-xl font-semibold shadow-lg"
            >
              <span v-if="!isLoading"><i class="fas fa-envelope text-white text-xl"></i> Envoyer le message</span>
              <span v-else class="flex items-center justify-center gap-2">
                <i class="fas fa-spinner animate-spin"></i> Envoi en cours...
              </span>
            </button>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* Style doux et cohérent */
input, textarea {
  transition: all 0.3s ease;
}

button:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}
</style>
