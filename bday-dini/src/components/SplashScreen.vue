<script setup>
defineEmits(['openMainScreen'])
</script>

<template>
  <section class="fixed inset-0 z-50 flex flex-col items-center justify-center bg-rose-50 bg-grid px-6 overflow-hidden">
    
    <!-- Emoji Melayang (Udah dibenerin dari yang corrupt) -->
    <div class="absolute top-20 left-10 text-4xl animate-float-slow opacity-80">✨</div>
    <div class="absolute top-40 right-12 text-3xl animate-float-fast opacity-80">💖</div>
    <div class="absolute bottom-32 left-16 text-2xl animate-float-slow opacity-80">🎂</div>
    <div class="absolute bottom-20 right-10 text-4xl animate-float-fast opacity-80">🎉</div>

    <!-- Main Card Soft Brutalism -->
    <div class="card-style bg-white p-10 text-center flex flex-col items-center relative z-10 animate-float">
      
      <p class="text-rose-500 text-xs tracking-[0.2em] uppercase font-extrabold mb-3">
        HAPPY BIRTHDAY! 🎉
      </p>
      
      <h1 class="text-5xl font-jakarta font-extrabold text-gray-800 leading-tight tracking-wide mb-8">
        Princess <br> <span class="text-rose-500">Dinii</span>
      </h1>
      
      <!-- Tombol Soft Brutalism dengan efek klik yang "Dalem" -->
      <button 
        @click="$emit('openMainScreen')"
        class="px-10 py-3 bg-rose-500 text-white rounded-xl tracking-[0.15em] uppercase font-extrabold transition-all duration-150 border-[3px] border-[#4C0519] shadow-[6px_6px_0px_0px_#4C0519] hover:bg-rose-400 active:translate-x-[6px] active:translate-y-[6px] active:shadow-none"
      >
        BUKA YAA 💖
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
  0%, 100% { transform: translateY(0) rotate(1deg); }
  50% { transform: translateY(-10px) rotate(-1deg); }
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