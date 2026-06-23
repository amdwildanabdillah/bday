<script setup>
defineEmits(['openMainScreen'])
</script>

<template>
  <section class="fixed inset-0 z-50 flex flex-col items-center justify-center bg-rose-50 bg-grid px-6 overflow-hidden">
    
    <div class="absolute top-20 left-10 text-4xl animate-float-slow opacity-80">🎈</div>
    <div class="absolute top-40 right-12 text-3xl animate-float-fast opacity-80">✨</div>
    <div class="absolute bottom-32 left-16 text-2xl animate-float-slow opacity-80">🌸</div>
    <div class="absolute bottom-20 right-10 text-4xl animate-float-fast opacity-80">🎉</div>

    <!-- Mengganti space-y-6 dengan flex dan gap yang lebih rapat -->
    <div class="text-center flex flex-col items-center relative z-10 bg-white/60 p-8 rounded-3xl backdrop-blur-sm border border-white/50 shadow-lg animate-float">
      
      <p class="text-rose-400 text-xs tracking-[0.2em] uppercase font-bold mb-1">
        HAPPY BIRTHDAY! 🎉
      </p>
      
      <h1 class="text-5xl font-cochin italic text-rose-600 leading-tight tracking-wide mb-8">
        Princess <br> Dinii
      </h1>
      
      <!-- Tombol di-uppercase dan font lebih tegas -->
      <button 
        @click="$emit('openMainScreen')"
        class="px-10 py-3 bg-rose-500 hover:bg-rose-400 text-white rounded-full tracking-[0.15em] uppercase font-extrabold transition-all duration-300 shadow-[0_8px_20px_rgba(244,63,94,0.4)] active:scale-95"
      >
        BUKA YAA ✨
      </button>

    </div>

  </section>
</template>

<style scoped>
.bg-grid {
  background-size: 35px 35px;
  background-image: 
    linear-gradient(to right, rgba(244, 63, 94, 0.08) 1px, transparent 1px),
    linear-gradient(to bottom, rgba(244, 63, 94, 0.08) 1px, transparent 1px);
}

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}
.animate-float { animation: float 4s ease-in-out infinite; }

@keyframes floatSlow {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  50% { transform: translateY(-15px) rotate(5deg); }
}
.animate-float-slow { animation: floatSlow 5s ease-in-out infinite; }

@keyframes floatFast {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  50% { transform: translateY(-10px) rotate(-5deg); }
}
.animate-float-fast { animation: floatFast 3s ease-in-out infinite; }
</style>