<script setup>
defineEmits(['openMainScreen'])
</script>

<template>
  <section class="fixed inset-0 z-50 flex flex-col items-center justify-center bg-rose-50 px-6 overflow-hidden">
    
    <div class="text-center space-y-6 animate-float relative z-10">
      <p class="text-rose-400 text-xs tracking-[0.2em] uppercase font-bold">
        HAPPY BIRTHDAY! 🎉
      </p>
      
      <h1 class="text-6xl font-fairy text-rose-600 leading-tight tracking-wide">
        Princess <br> Dinii
      </h1>
      
      <button 
        @click="$emit('openMainScreen')"
        class="mt-12 px-10 py-3 bg-rose-500 hover:bg-rose-400 text-white rounded-full tracking-wider font-semibold transition-all duration-300 shadow-[0_8px_20px_rgba(244,63,94,0.4)] active:scale-95"
      >
        Buka yaa ✨
      </button>
    </div>

  </section>
</template>

<style scoped>
@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}
.animate-float { animation: float 4s ease-in-out infinite; }
</style>