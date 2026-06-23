<script setup>
import { ref, onMounted } from 'vue'
import 'vue3-carousel/dist/carousel.css'
import { Carousel, Slide } from 'vue3-carousel'

defineProps({
  photoList: Array,
  isFetching: Boolean
})

const emit = defineEmits(['triggerAudio'])
const carouselRef = ref(null)

const formatCaption = (filename) => {
  if (!filename) return ''
  let text = filename.split('.').slice(0, -1).join('.')
  text = text.replace(/^\d+[-_]/, '')
  text = text.replace(/[-_]/g, ' ')
  return text
}

onMounted(() => {
  const observer = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) {
      emit('triggerAudio') 
      observer.disconnect() 
    }
  }, { threshold: 0.3 }) 

  if (carouselRef.value) {
    observer.observe(carouselRef.value)
  }
})
</script>

<template>
  <section ref="carouselRef" class="py-12 w-full flex flex-col justify-center relative overflow-hidden">
    
    <div class="absolute top-10 right-8 text-2xl animate-pulse opacity-60">✨</div>
    <div class="absolute bottom-20 left-6 text-xl animate-bounce opacity-60">💖</div>

    <!-- Judul dengan Kotak Section Bergaya Soft Brutalism -->
    <div class="px-6 mb-10 text-center relative z-10 flex justify-center mt-4">
      <div class="card-style bg-rose-50 px-8 py-5 relative inline-block transform -rotate-1">
        
        <!-- Ikon Kamera Jadi Badge Melayang -->
        <div class="absolute -top-5 -right-4 bg-white text-3xl p-2 rounded-full border-[3px] border-[#4C0519] shadow-[4px_4px_0px_0px_#4C0519] rotate-12 z-20">
          📸
        </div>

        <h2 class="text-3xl font-jakarta font-extrabold text-gray-800 drop-shadow-sm">
          Princess <span class="text-rose-500">Dini</span>
        </h2>
        
        <!-- Garis putus-putus pembatas -->
        <div class="border-t-2 border-dashed border-rose-300 my-2"></div>
        
        <p class="text-rose-500 text-xs font-bold tracking-widest uppercase">
          Dengan berbagai mood nya..
        </p>
      </div>
    </div>

    <div v-if="isFetching" class="px-6 text-rose-500 font-bold text-sm animate-pulse text-center relative z-10">
      Memuat Foto Princess Dini...
    </div>

    <!-- Carousel Infinity Asli pakai vue3-carousel -->
    <Carousel v-else :items-to-show="1.2" :wrap-around="true" :autoplay="3000" class="px-4 relative z-10">
      <Slide v-for="(photo, index) in photoList" :key="index">
        <div class="p-3 w-full pb-8">
          
          <!-- Card Foto Soft Brutalism -->
          <div class="card-style bg-white p-3 h-full transition-transform hover:scale-[1.02]">
            <!-- Selotip Estetik -->
            <div class="absolute -top-3 left-1/2 -translate-x-1/2 w-14 h-4 bg-white/70 backdrop-blur-sm border border-[#4C0519] shadow-[2px_2px_0px_0px_#4C0519] rotate-[-4deg] z-20"></div>
            
            <img 
              :src="photo.url" 
              alt="Memory" 
              loading="lazy"
              class="w-full h-[40vh] object-cover rounded-sm border-2 border-rose-100"
            />
            
            <!-- Caption Center & Auto-Wrap -->
            <p class="mt-4 pb-2 font-jakarta uppercase text-rose-600 text-[15px] font-bold text-center leading-snug break-words px-2">
              {{ formatCaption(photo.filename) }}
            </p>
          </div>

        </div>
      </Slide>
    </Carousel>

  </section>
</template>