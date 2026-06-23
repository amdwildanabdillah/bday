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
      <div class="absolute inset-0 bg-gradient-to-t from-rose-50 via-rose-50/20 to-transparent"></div>
    </div>

    <div class="relative z-10 w-full animate-slide-up">
      <p class="text-rose-600 text-xs tracking-[0.2em] uppercase mb-2 font-bold drop-shadow-sm">
        Level 21 Unlocked 🎂
      </p>
      <h1 class="text-6xl font-fairy text-gray-900 leading-tight drop-shadow-md">
        Happy <br> 
        <span class="text-rose-500 text-7xl drop-shadow-sm">21st</span> <br>
        Birthday!
      </h1>
    </div>
  </section>
</template>