<script setup>
import { ref } from 'vue'

// Data 3 Video Kamu
const videoList = ref([
  {
    id: 1,
    title: 'Komang',
    // Masukin FULL URL dari R2 atau Supabase di sini
    videoUrl: 'https://pub-bfe7d1d83328475693640e5f60e060e8.r2.dev/vlog%20ala.mp4', 
    caption: 'Kalo kata komang "Sebab kau terlalu indah dari sekedar kata"'
  },
  {
    id: 2,
    title: 'Cerita Tentang Kita',
    videoUrl: 'https://pub-bfe7d1d83328475693640e5f60e060e8.r2.dev/Vlog%20Ala%20Ala.mp4', 
    caption: 'Dari kejauhan, tergambar cerita tentang kita ✨'
  },
  {
    id: 3,
    title: 'Everything You Are',
    videoUrl: '', 
    caption: 'Tonton sampai habis yaa 🎬'
  }
])
</script>

<template>
  <section class="py-12 w-full flex flex-col justify-center relative overflow-hidden">
    
    <div class="px-6 mb-8 text-center relative z-10">
      <h2 class="text-3xl font-cochin font-semibold text-rose-500 drop-shadow-sm">
        Special Bonus 🎬
      </h2>
      <p class="text-gray-600 text-xs mt-1 font-bold tracking-wide">Beberapa memori lagi nih...</p>
    </div>

    <div class="flex overflow-x-auto gap-6 px-8 pb-12 snap-x snap-mandatory scrollbar-hide relative z-10 items-center">
      
      <div 
        v-for="(video, index) in videoList" 
        :key="video.id"
        class="shrink-0 w-[75vw] bg-white p-3 pb-14 snap-center relative shadow-[0_10px_25px_rgba(244,63,94,0.15)] border border-gray-100 transition-transform duration-300 hover:scale-105"
        :class="index % 2 === 0 ? 'rotate-1 rounded-2xl' : '-rotate-1 rounded-2xl'"
      >
        <div class="absolute -top-3 left-1/2 -translate-x-1/2 w-14 h-4 bg-white/70 backdrop-blur-sm border border-gray-200 shadow-sm rotate-[-2deg] z-30"></div>
        
        <div class="relative w-full aspect-[9/16] bg-gray-900 rounded-lg overflow-hidden shadow-inner z-20">
          
          <!-- Langsung panggil URL dari R2 / Supabase -->
          <video 
            v-if="video.videoUrl"
            controls
            controlsList="nodownload"
            preload="metadata"
            class="w-full h-full object-cover"
            :src="video.videoUrl"
          ></video>
          
          <div v-else class="w-full h-full flex flex-col items-center justify-center bg-gray-800 text-rose-400">
            <span class="text-4xl mb-2">🎥</span>
            <p class="text-xs font-jakarta tracking-wide">Menunggu memori...</p>
          </div>

        </div>

        <p class="absolute bottom-3 left-0 w-full text-center font-cochin italic text-rose-500 text-[15px] font-medium px-3 leading-snug line-clamp-2">
          {{ video.caption }}
        </p>
      </div>

    </div>

  </section>
</template>