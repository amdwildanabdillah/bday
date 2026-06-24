<script setup>
import { ref } from 'vue'

const messages = ref([
  {
    id: 1,
    title: 'Congrats Gurlll !',
    icon: '🎉',
    color: 'rose',
    closedText: 'Ini dibuka pertama yaa 👀', // <-- Ini buat tulisan pas ketutup
    text: 'Baarakallah Fii Umrik Princess Dinii, selamat ulang tahun yang ke 21. Selamat tambah umur dan bahagia... wkwkwkwkwkwk. selamat memasuki dan menempuh fase selanjutnya.'
  },
  {
    id: 2,
    title: 'Pray & Wishes',
    icon: '🌟',
    color: 'pink',
    closedText: 'Terus iniii ✨', // <-- Tulisan kartu kedua
    text: 'Semoga di umur yang baru tambahini, segala hal baik selalu mengiringi langkah kaki pendekmu wkwkw. Serius, Semoga segala harapan dan impianmu terwujud, Datang hal-hal baik, semoga nasi mu selalu hangat, tidurmu selalu pulas, hari mu selalu baik dan lancar. Semoga hari-harimu selalu diiringi cinta yang gaada habisnya. Dijauhkan dari hal hal buruk. Semoga bisa mendapatkan hal hal yang selama ini diperjuangkan, my best wishes for u.'
  },
  {
    id: 3,
    title: 'Advice',
    icon: '💌',
    color: 'red',
    closedText: 'Ini jugaa 💌', // <-- Tulisan kartu ketiga
    text: 'Kurang-kurangin jajan sembarangan-nya yaa. Dibenerin pola makan, pola hidupnya. Perbanyak istirahat, jangan terlalu keras sama diri sendiri. Bisa lebih menghargai orang lain ya din... Bisa lebih sabar, lebih tabah, ga marah marah wkwkwkwk. Tetap semangat, You got this Princess.'
  }
])

const openStates = ref([false, false, false])

const toggleMessage = (index) => {
  openStates.value[index] = !openStates.value[index]
}
</script>

<template>
  <div class="px-6 space-y-8 relative z-10 pt-6">
    <div 
      v-for="(msg, index) in messages" 
      :key="msg.id"
      class="relative transition-all duration-500 ease-in-out cursor-pointer"
      @click="toggleMessage(index)"
    >
      
      <!-- Ikon Badge Melayang -->
      <div class="absolute -top-6 -left-3 bg-white text-3xl p-2 rounded-full border-[3px] border-[#4C0519] shadow-[4px_4px_0px_0px_#4C0519] z-20 rotate-[-10deg] hover:rotate-0 transition-transform">
        {{ msg.icon }}
      </div>

      <!-- Card Tertutup -->
      <div 
        v-if="!openStates[index]"
        class="card-style bg-rose-50 p-6 text-center hover:scale-[1.02] transition-transform"
      >
        <!-- Manggil text custom sesuai index-nya -->
        <h3 class="font-jakarta font-extrabold text-gray-800 tracking-wide mt-2">
          {{ msg.closedText }}
        </h3>
      </div>

      <!-- Card Terbuka -->
<div 
  v-else
  class="card-style bg-white p-6 relative overflow-hidden animate-fade-in flex flex-col items-start"
>
  <!-- Judul dipaksa rata kiri -->
  <h3 :class="`font-jakarta font-extrabold text-xl text-${msg.color}-600 mb-3 mt-2 relative z-10 w-full text-left`">
    {{ msg.title }}
  </h3>
  
  <!-- Garis pembatas dipaksa penuh (w-full) -->
  <div class="border-t-2 border-dashed border-rose-200 my-3 w-full"></div>
  
  <!-- Teks pesan dipaksa rata kiri -->
  <p class="font-jakarta text-gray-700 text-[13px] leading-relaxed font-semibold relative z-10 w-full text-left">
    {{ msg.text }}
  </p>
</div>
    </div>
  </div>
</template>

<style>
@keyframes fadeIn { 
  from { opacity: 0; transform: translateY(10px); } 
  to { opacity: 1; transform: translateY(0); } 
}
.animate-fade-in { 
  animation: fadeIn 0.5s ease-out forwards; 
}
</style>