<script setup>
import { ref } from 'vue'

// Emit buat ngirim sinyal ke App.vue kalau video diputar
const emit = defineEmits(['videoPlayed'])

// Cukup SATU KALI aja nulisnya wkwkwk
const isNoteOpen = ref(false)

const videoList = ref([
  {
    id: 1,
    title: 'Komang',
    videoUrl: 'https://pub-bfe7d1d83328475693640e5f60e060e8.r2.dev/vlog%20ala.mp4', 
    caption: 'Sebab kau terlalu indah dari sekedar kata'
  },
  {
    id: 2,
    title: 'Message in A Bottle',
    videoUrl: 'https://pub-bfe7d1d83328475693640e5f60e060e8.r2.dev/_storage_emulated_0_DCIM_Camera_lv_0_20251008014601.mp4', 
    caption: 'Cause u could be the one that I love'
  },
  {
    id: 3,
    title: 'Everything You Are',
    videoUrl: 'https://pub-bfe7d1d83328475693640e5f60e060e8.r2.dev/everiting.mp4', 
    caption: 'Everything U Are apa U Are Everything ?'
  }
])
</script>

<template>
  <section class="py-12 w-full flex flex-col justify-center relative overflow-hidden">
    
    <!-- Judul dengan Kotak Section Bergaya Soft Brutalism -->
    <div class="px-6 mb-10 text-center relative z-10 flex justify-center">
      <!-- padding horizontal ditambah (px-10) biar lega -->
      <div class="card-style bg-rose-50 px-10 py-5 relative inline-block transform rotate-1">
        
        <!-- Ikon Clapperboard digeser lebih jauh (-left-6, -top-6) biar B-nya kelihatan -->
        <div class="absolute -top-6 -left-6 bg-white text-3xl p-2 rounded-full border-[3px] border-[#4C0519] shadow-[4px_4px_0px_0px_#4C0519] -rotate-12 z-20">
          🎬
        </div>

        <h2 class="text-3xl font-jakarta font-extrabold text-gray-800 drop-shadow-sm">
          Best <span class="text-rose-500">Video</span>
        </h2>
        
        <div class="border-t-2 border-dashed border-rose-300 my-2"></div>
        
        <p class="text-rose-500 text-xs font-bold tracking-widest uppercase">
          of Princess Dini
        </p>
      </div>
    </div>

    <!-- Bagian Video Carousel -->
    <div class="flex overflow-x-auto gap-6 px-8 pb-12 snap-x snap-mandatory scrollbar-hide relative z-10 items-center">
      <div 
        v-for="(video, index) in videoList" 
        :key="video.id"
        class="shrink-0 w-[75vw] card-style bg-white p-3 pb-6 snap-center relative transition-transform duration-300 hover:scale-[1.02]"
      >
        <div class="absolute -top-3 left-1/2 -translate-x-1/2 w-14 h-4 bg-white/70 backdrop-blur-sm border border-[#4C0519] shadow-[2px_2px_0px_0px_#4C0519] rotate-[-2deg] z-30"></div>
        
        <div class="relative w-full aspect-[9/16] bg-gray-900 rounded-lg overflow-hidden border-2 border-rose-100 z-20">
          <video 
  v-if="video.videoUrl" 
  controls controlsList="nodownload" preload="metadata" 
  class="w-full h-full object-cover" 
  :src="video.videoUrl"
  @play="$emit('videoPlayed')" 
></video>
          <div v-else class="w-full h-full flex flex-col items-center justify-center bg-gray-800 text-rose-400">
            <span class="text-4xl mb-2">🎥</span>
            <p class="text-xs font-jakarta tracking-wide">Menunggu memori...</p>
          </div>
        </div>
        
        <p class="mt-4 font-jakarta text-rose-600 text-[15px] font-bold text-center leading-snug break-words px-2 capitalize">
          {{ video.caption }}
        </p>
      </div>
    </div>

    <!-- Bagian Galeri Chaotic & Penutup (Interactive) -->
    <div class="px-6 py-8 relative z-10">
      <h3 class="text-xl font-jakarta font-extrabold text-gray-800 mb-8 text-center tracking-widest uppercase">— Last —</h3>
      
      <div class="grid grid-cols-2 gap-4 mb-10">
        <div class="card-style aspect-[3/4] overflow-hidden rotate-[-3deg]">
          <img src="https://pub-bfe7d1d83328475693640e5f60e060e8.r2.dev/ANZ00122.jpg" class="w-full h-full object-cover">
        </div>
        <div class="card-style aspect-[3/4] overflow-hidden rotate-[2deg] translate-y-4">
          <img src="https://pub-bfe7d1d83328475693640e5f60e060e8.r2.dev/_SNP0090.jpg" class="w-full h-full object-cover">
        </div>
      </div>

      <!-- Note yang bisa di-klik dengan Wrapper Relatif -->
      <div class="relative mt-8">
        
        <!-- Ikon Amplop Melayang (Akhirnya pisah kos juga) -->
        <div class="absolute -top-6 -left-3 bg-white text-3xl p-2 rounded-full border-[3px] border-[#4C0519] shadow-[4px_4px_0px_0px_#4C0519] -rotate-12 z-20 animate-pulse">
          ✉️
        </div>

        <div 
          class="card-style bg-rose-50 p-8 pt-10 text-center cursor-pointer transition-all duration-300 hover:scale-[1.02]"
          @click="isNoteOpen = !isNoteOpen"
        >
          <!-- Kondisi Tertutup -->
          <div v-if="!isNoteOpen">
            <p class="text-gray-800 font-jakarta font-extrabold text-lg">
              Dari Hati Bangetttt 💖
            </p>
          </div>

          <!-- Kondisi Terbuka -->
          <div v-else class="animate-fade-in flex flex-col items-start text-left">
            <p class="font-jakarta text-gray-700 leading-relaxed font-semibold text-[14px] whitespace-preline">
              "Sebelomnya, maap yaa bahannya ini tok wkwkwk, ini juga dari file file lama, nyari nyari di galeri, di adobe cloud, di drive, sama ambil dari feed ig mu satu xixixixi.
              <br><br>
              Maap juga kalo foto videonya ini ini aja, gaada bahan lagi soalnya hehe, ini buate juga agak buru-buru, tapi tulus kok rill no fek fek.
              <br><br>
              Oiyaa, ini gatau video e bisa dibuka lancar apa ngga, kalo kamu cerita sinyale susah, kayae agak lemot hehe.
              <br><br>

              Maap yaa... selama kita temenan, sering njaraki kamu, sering bikin betmut, bikin nggaenak, mungkin bikin nangis. <br><br>
              Maaf kalo sikapku sering bikin bingung ke kamu juga mungkin, maaf sempet bentak kamu juga waktu itu..<br><br>
              Tetep jadi dini yang baik ya, Makasih tetep mau respon hehe, thanks buat semuanya..<br><br>
              Tetep bahagia dan senyum ya din, asli muanis cuantik ga boong hehe.. nek mara mara mrengut ilang ayu ne ✌"
            </p>
            <div class="border-t-2 border-dashed border-rose-300 my-5 w-full"></div>
            <span class="text-rose-600 font-extrabold tracking-widest text-sm uppercase">— Tom —</span>
          </div>
        </div>
      </div>

    </div>
  </section>
</template>