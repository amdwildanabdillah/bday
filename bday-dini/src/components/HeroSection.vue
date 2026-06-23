<script setup>
defineProps({
  heroImage: String
})
</script>

<template>
  <section class="relative h-[85vh] w-full flex flex-col justify-end px-6 pb-20">
    <div class="absolute inset-0 z-0">
      <img 
        v-if="heroImage"
        :src="heroImage" 
        alt="Hero Cover" 
        class="w-full h-full object-cover opacity-100 object-center" 
      />
      <!-- Gradient dipendekkan cuma setengah bawah (h-1/2) -->
      <div class="absolute inset-x-0 bottom-0 h-1/2 bg-gradient-to-t from-rose-50 via-rose-50/60 to-transparent"></div>
    </div>

    <div class="relative z-10 w-full animate-slide-up">
      <!-- Baarakallah dikasih background pill transparan biar mencolok -->
      <div class="inline-block bg-white/60 backdrop-blur-sm px-4 py-2 rounded-full mb-4 shadow-sm border border-white/50">
        <p class="text-rose-600 text-xs tracking-[0.2em] uppercase font-bold drop-shadow-sm m-0">
          Baarakallah Fii Umrik 🎂
        </p>
      </div>
      
      <!-- Layout Flex Kiri-Kanan -->
      <div class="flex items-center justify-between w-full">
        <h1 class="text-4xl font-jakarta font-extrabold text-gray-800 leading-snug drop-shadow-md">
          Happy <br> Birthday!
        </h1>
        <span class="text-rose-500 font-cochin italic text-7xl drop-shadow-sm font-bold pr-2">
          21st
        </span>
      </div>
    </div>
  </section>
</template>