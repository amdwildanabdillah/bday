<script setup>
import { ref, onMounted } from 'vue'
import { supabase } from './utils/supabase'

import SplashScreen from './components/SplashScreen.vue'
import HeroSection from './components/HeroSection.vue'
import MessageSection from './components/MessageSection.vue'
import CarouselSection from './components/CarouselSection.vue'
import VideoSection from './components/VideoSection.vue'

const isOpened = ref(false) 
const heroImage = ref('')
const photoList = ref([])
const isFetching = ref(true)

// Referensi Audio
const audioHbd = ref(null)
const audioCjr = ref(null)

const fetchPhotos = async () => {
  // Ambil Cover
  const { data: coverFiles } = await supabase.storage.from('bday-gallery').list('cover', { limit: 1 })
  if (coverFiles && coverFiles.length > 0 && coverFiles[0].name !== '.emptyFolderPlaceholder') {
    const { data } = supabase.storage.from('bday-gallery').getPublicUrl(`cover/${coverFiles[0].name}`)
    heroImage.value = data.publicUrl
  }

  // Ambil Gallery
  const { data: galleryFiles } = await supabase.storage.from('bday-gallery').list('gallery', { limit: 100 })
  photoList.value = galleryFiles
    .filter(file => file.name !== '.emptyFolderPlaceholder') 
    .map(file => {
      const { data } = supabase.storage.from('bday-gallery').getPublicUrl(`gallery/${file.name}`)
      return {
        url: data.publicUrl,
        filename: file.name
      }
    })
  isFetching.value = false
}

const openSurprise = () => {
  isOpened.value = true
  window.scrollTo(0, 0)
  
  if(audioHbd.value) {
    audioHbd.value.volume = 0.5 
    audioHbd.value.play()
  }
}

const switchToCjr = () => {
  if(audioHbd.value && audioCjr.value) {
    audioHbd.value.pause() 
    audioCjr.value.volume = 0.8 
    audioCjr.value.play() 
  }
}

onMounted(() => {
  fetchPhotos() 
})
</script>

<template>
  <main class="bg-rose-50 text-gray-800 font-jakarta overflow-x-hidden w-full min-h-screen bg-pattern">
    
    <audio ref="audioHbd" src="/hbd.mp3"></audio>
    <audio ref="audioCjr" src="/cjr.mp3"></audio>

    <transition leave-active-class="transition-all duration-1000 ease-in-out" leave-to-class="opacity-0 scale-110">
      <SplashScreen v-if="!isOpened" @openMainScreen="openSurprise" />
    </transition>

    <div v-if="isOpened" class="animate-fade-in">
      <HeroSection :heroImage="heroImage" />
      <MessageSection />
      <CarouselSection :photoList="photoList" :isFetching="isFetching" @triggerAudio="switchToCjr" />
      <VideoSection />
      
      <footer class="pb-12 text-center relative z-10">
        <p class="text-rose-400 text-xs font-medium tracking-widest uppercase">✨ Made with love hihi ✨</p>
      </footer>
    </div>

  </main>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:ital,wght@0,300..800;1,300..800&display=swap');

/* Font Baru */
.font-cochin { font-family: 'Cochin', Georgia, serif; }
.font-jakarta { font-family: 'Plus Jakarta Sans', sans-serif; }

/* CSS Untuk Ornamen Background Titik-Titik Estetik */
.bg-pattern {
  background-image: radial-gradient(var(--tw-colors-rose-200) 1px, transparent 1px);
  background-size: 24px 24px;
}

.scrollbar-hide::-webkit-scrollbar { display: none; }
.scrollbar-hide { -ms-overflow-style: none; scrollbar-width: none; }
@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
.animate-fade-in { animation: fadeIn 1s ease-in-out forwards; }
</style>