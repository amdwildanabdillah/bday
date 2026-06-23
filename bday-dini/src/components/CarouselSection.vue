<script setup>
import { ref, onMounted } from 'vue'

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

    <div class="px-6 mb-8 text-center relative z-10">
      <h2 class="text-3xl font-fairy text-gray-800 drop-shadow-sm">
        Princess <span class="text-rose-500">Dini</span> 📸
      </h2>
      <p class="text-rose-400 text-xs mt-1 font-bold tracking-wide">Dengan semua mood nya..</p>
    </div>

    <div v-if="isFetching" class="px-6 text-rose-400 text-sm animate-pulse text-center relative z-10">
      Memuat Foto Princess Dini
    </div>

    <div v-else class="flex overflow-x-auto gap-6 px-8 pb-12 snap-x snap-mandatory scrollbar-hide relative z-10 items-center">
      <div 
        v-for="(photo, index) in photoList" 
        :key="index"
        class="shrink-0 w-[70vw] h-[45vh] bg-white p-3 pb-14 snap-center relative shadow-[0_10px_25px_rgba(244,63,94,0.15)] border border-gray-100 transition-transform duration-300 hover:scale-105"
        :class="index % 2 === 0 ? 'rotate-2 rounded-sm' : '-rotate-2 rounded-md'"
      >
        <div class="absolute -top-3 left-1/2 -translate-x-1/2 w-14 h-4 bg-white/70 backdrop-blur-sm border border-gray-200 shadow-sm rotate-[-4deg] z-20"></div>
        
        <img 
          :src="photo.url" 
          alt="Memory" 
          loading="lazy"
          class="w-full h-full object-cover rounded-sm shadow-inner"
        />
        
        <!-- Font dikecilin jadi 15px, truncate dihapus ganti line-clamp-2 biar bisa 2 baris -->
        <p class="absolute bottom-2 left-0 w-full text-center font-cochin italic text-rose-500 text-[15px] font-medium px-3 leading-snug line-clamp-2">
          {{ formatCaption(photo.filename) }}
        </p>
      </div>
    </div>
  </section>
</template>