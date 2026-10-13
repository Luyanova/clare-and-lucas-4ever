<template>
  <section class="relative bg-[#0D0A1A] py-24 md:py-32 px-6 overflow-hidden">
    <!-- Background glows -->
    <div class="absolute top-0 left-1/3 w-[500px] h-[500px] bg-[#E8A0BF]/5 rounded-full blur-[140px] pointer-events-none"></div>
    <div class="absolute bottom-0 right-1/4 w-[400px] h-[400px] bg-[#C2B5E8]/5 rounded-full blur-[120px] pointer-events-none"></div>

    <!-- Header -->
    <div class="text-center mb-16 md:mb-20 relative z-10">
      <span class="section-subtitle text-[#E8A0BF]/50 text-xs uppercase tracking-[0.3em] mb-4 block">ce que je ressens</span>
      <h2 class="section-title text-[#EDE8F5] text-4xl md:text-5xl lg:text-6xl">Pourquoi je t'aime</h2>
      <div class="mt-6 mx-auto w-16 h-px bg-gradient-to-r from-transparent via-[#E8A0BF]/40 to-transparent"></div>
    </div>

    <div class="flex flex-col items-center gap-10 relative z-10">
      <!-- Dispenser Button -->
      <button
        @click="dispenseTicket"
        class="group relative px-8 py-4 rounded-2xl cursor-pointer overflow-hidden transition-all duration-500 hover:scale-[1.03] active:scale-95"
      >
        <!-- Button bg gradient -->
        <div class="absolute inset-0 bg-gradient-to-r from-[#C2B5E8] via-[#D4A8D0] to-[#E8A0BF] rounded-2xl"></div>
        <!-- Shimmer overlay -->
        <div class="absolute inset-0 bg-gradient-to-r from-transparent via-white/15 to-transparent -translate-x-full group-hover:translate-x-full transition-transform duration-1000 ease-out"></div>
        <!-- Glow -->
        <div class="absolute inset-0 rounded-2xl shadow-[0_0_40px_rgba(194,181,232,0.3)] group-hover:shadow-[0_0_60px_rgba(194,181,232,0.5)] transition-shadow duration-500"></div>
        <!-- Text -->
        <span class="relative z-10 flex items-center gap-3 text-[#0D0A1A] font-semibold text-base tracking-wide">
          <span class="text-lg">✦</span>
          Tirer un ticket
          <svg class="w-4 h-4 group-hover:translate-y-0.5 transition-transform duration-300" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
            <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7" />
          </svg>
        </span>
      </button>

      <!-- Ticket -->
      <Transition name="ticket">
        <div
          v-if="showTicket"
          :key="currentTicketIndex"
          class="relative max-w-sm w-full"
        >
          <!-- Ticket card -->
          <div class="relative bg-[#16112A] rounded-2xl border border-[#C2B5E8]/15 overflow-hidden shadow-[0_20px_60px_rgba(0,0,0,0.4)]">
            <!-- Top decorative strip -->
            <div class="h-1 bg-gradient-to-r from-[#C2B5E8] via-[#E8A0BF] to-[#F0C4A0]"></div>

            <!-- Perforation line top -->
            <div class="flex items-center justify-center gap-2 py-2">
              <span v-for="i in 20" :key="'t'+i" class="block w-1.5 h-px bg-[#C2B5E8]/15 rounded-full"></span>
            </div>

            <!-- Content -->
            <div class="px-8 py-6 text-center">
              <!-- Number -->
              <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-[#C2B5E8]/8 border border-[#C2B5E8]/10 mb-5">
                <span class="text-[#C2B5E8]/50 text-[10px] font-semibold tracking-[0.2em] uppercase">Raison nº{{ currentTicketIndex + 1 }}</span>
              </div>

              <!-- Quote -->
              <p class="text-[#EDE8F5] text-base md:text-lg leading-relaxed font-light italic">
                "{{ compliments[currentTicketIndex].text }}"
              </p>

              <!-- Emoji -->
              <div class="mt-5 text-3xl">{{ compliments[currentTicketIndex].emoji }}</div>
            </div>

            <!-- Perforation line bottom -->
            <div class="flex items-center justify-center gap-2 py-2">
              <span v-for="i in 20" :key="'b'+i" class="block w-1.5 h-px bg-[#C2B5E8]/15 rounded-full"></span>
            </div>

            <!-- Bottom strip -->
            <div class="h-1 bg-gradient-to-r from-[#F0C4A0] via-[#E8A0BF] to-[#C2B5E8]"></div>

            <!-- Corner accents -->
            <div class="absolute top-0 left-0 w-16 h-16 bg-gradient-to-br from-[#C2B5E8]/5 to-transparent pointer-events-none"></div>
            <div class="absolute bottom-0 right-0 w-16 h-16 bg-gradient-to-tl from-[#E8A0BF]/5 to-transparent pointer-events-none"></div>
          </div>

          <!-- Ambient glow beneath ticket -->
          <div class="w-2/3 mx-auto h-12 -mt-6 bg-[#C2B5E8]/8 rounded-full blur-[30px]"></div>
        </div>
      </Transition>

    
      
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface Compliment {
  text: string
  emoji: string
}

const compliments: Compliment[] = [
  { text: 'You\'re a good girl.', emoji: '🌸' },
  { text: 'Tu es parfaite, je ne peux jamais m\'arrêter de penser à chaques choses qui te.', emoji: '💫' },
  { text: 'Chaque jours tu me suprends avec un style encore plus fou, tu es la reine des baddies.', emoji: '✨' },
  { text: 'Te savoir heureuse est ma priorité.', emoji: '🌙' },
  { text: 'Je veux construire une vie d\'amour avec toi.', emoji: '🦋' },
  { text: 'Je vois ton visagz chaque nuits.', emoji: '🌹' },
  { text: 'J\'aime trop te voir te serrer dans mes bras devant un bon animé.', emoji: '💕' },
  { text: 'Tu rends toutes les autres filles moches, je ne vois que toi.', emoji: '🌺' },
]

const showTicket = ref(false)
const currentTicketIndex = ref(0)
const isDispensing = ref(false)

function dispenseTicket() {
  if (isDispensing.value) return

  if (!showTicket.value) {
    currentTicketIndex.value = 0
    showTicket.value = true
    return
  }

  isDispensing.value = true
  showTicket.value = false
  setTimeout(() => {
    currentTicketIndex.value = (currentTicketIndex.value + 1) % compliments.length
    showTicket.value = true
    setTimeout(() => {
      isDispensing.value = false
    }, 300)
  }, 250)
}
</script>

<style scoped>
.ticket-enter-active {
  transition: all 0.6s cubic-bezier(0.34, 1.56, 0.64, 1);
}
.ticket-leave-active {
  transition: all 0.25s cubic-bezier(0.4, 0, 1, 1);
}
.ticket-enter-from {
  opacity: 0;
  transform: translateY(-40px) scale(0.92) rotate(-1deg);
}
.ticket-leave-to {
  opacity: 0;
  transform: translateY(20px) scale(0.96);
}
</style>
