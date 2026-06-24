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

// Referensi Audio (Tinggal 1 aja)
const bgMusic = ref(null)

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
  
  // Mainkan lagu utamanya pas Splash Screen di-klik
  if(bgMusic.value) {
    bgMusic.value.volume = 0.5 
    bgMusic.value.play()
  }
}

// Fungsi baru buat matiin lagu pas video nyala
const pauseAudio = () => {
  if(bgMusic.value) {
    bgMusic.value.pause() 
  }
}

onMounted(() => {
  fetchPhotos() 
})
</script>

<template>
  <main class="bg-rose-50 text-gray-800 font-jakarta overflow-x-hidden w-full min-h-screen relative">
    
    <!-- Aksen Background Soft Brutalism (Biar gak sepi) -->
    <div class="fixed top-32 left-10 text-5xl text-rose-300 rotate-12 z-0 opacity-50 animate-pulse">✦</div>
    <div class="fixed bottom-40 right-12 text-6xl text-rose-300 -rotate-12 z-0 opacity-50 animate-bounce">✱</div>
    <div class="fixed top-1/2 -left-8 w-16 h-16 bg-white border-[3px] border-[#4C0519] shadow-[4px_4px_0px_0px_#4C0519] rounded-xl rotate-45 z-0 opacity-40"></div>

    <!-- Audio cuma sisa satu -->
    <audio ref="bgMusic" src="/lagu-tiktok.mp3" loop></audio>

    <transition leave-active-class="transition-all duration-1000 ease-in-out" leave-to-class="opacity-0 scale-110">
      <SplashScreen v-if="!isOpened" @openMainScreen="openSurprise" />
    </transition>

    <div v-if="isOpened" class="animate-fade-in relative z-10">
      <HeroSection :heroImage="heroImage" />
      <MessageSection />
      
      <!-- Carousel udah gak manggil audio lagi -->
      <CarouselSection :photoList="photoList" :isFetching="isFetching" />
      
      <!-- Tambahin event pause lagunya ke VideoSection -->
      <VideoSection @videoPlayed="pauseAudio" />
      
      <!-- Footer Stiker Soft Brutalism -->
      <footer class="pb-12 text-center relative z-10 flex justify-center mt-8">
        <div class="card-style bg-rose-50 px-6 py-2 inline-block transform rotate-[-2deg] active:scale-95 transition-all duration-150">
          <p class="text-rose-600 text-xs font-jakarta font-extrabold tracking-widest uppercase m-0">
            ✨ Made with love hihi ✨
          </p>
        </div>
      </footer>
    </div>

  </main>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:ital,wght@0,300..800;1,300..800&display=swap');

/* Font Baku */
.font-jakarta { font-family: 'Plus Jakarta Sans', sans-serif; }

/* CSS Global Soft Brutalism */
:root {
  --border-color: #4C0519;
}

.card-style {
  background-color: white;
  border: 3px solid var(--border-color);
  border-radius: 16px;
  box-shadow: 6px 6px 0px 0px var(--border-color);
  transition: all 0.2s ease-in-out;
}

/* Biar background ada pattern grid halus titik-titik */
main {
  background-image: radial-gradient(var(--tw-colors-rose-200) 1px, transparent 1px);
  background-size: 24px 24px;
}

.scrollbar-hide::-webkit-scrollbar { display: none; }
.scrollbar-hide { -ms-overflow-style: none; scrollbar-width: none; }
@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
.animate-fade-in { animation: fadeIn 1s ease-in-out forwards; }
</style>