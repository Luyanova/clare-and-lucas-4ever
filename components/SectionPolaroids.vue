<template>
  <section class="relative bg-[#110E20] py-24 md:py-32 px-6 overflow-hidden">
    <!-- Background effects -->
    <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[600px] bg-[#E8A0BF]/5 rounded-full blur-[150px] pointer-events-none"></div>

    <!-- Header -->
    <div class="text-center mb-16 md:mb-20 relative z-10">
      <span class="section-subtitle text-[#E8A0BF]/50 text-xs uppercase tracking-[0.3em] mb-4 block">quelques moments sympas sur des milliers</span>
      <h2 class="section-title text-[#EDE8F5] text-4xl md:text-5xl lg:text-6xl">Nos Souvenirs</h2>
      <div class="mt-6 mx-auto w-16 h-px bg-gradient-to-r from-transparent via-[#E8A0BF]/40 to-transparent"></div>
    </div>

    <!-- Polaroid Grid -->
    <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-5 md:gap-7 max-w-5xl mx-auto relative z-10">
      <div
        v-for="(card, index) in polaroidCards"
        :key="index"
        class="group cursor-pointer select-none animate-hover-float"
        :style="{ perspective: '1200px', animationDelay: `${index * 0.3}s` }"
        @click="flipCard(index)"
      >
        <div
          :class="[
            'card-inner relative w-full',
            card.flipped ? 'flip-active' : ''
          ]"
        >
          <!-- FRONT -->
          <div class="backface-hidden relative rounded-2xl" style="-webkit-backface-visibility: hidden; backface-visibility: hidden;">
            <!-- Photo area -->
            <div class="card-border bg-[#1A1530] p-3 pb-14 rounded-2xl border border-[#C2B5E8]/8 transition-all duration-500 shadow-[0_4px_24px_rgba(0,0,0,0.3)] overflow-hidden">
              <div class="relative aspect-square rounded-xl overflow-hidden bg-[#0D0A1A]">
                <nuxt-img
                  :src="card.image"
                  :alt="card.caption"
                  draggable="false"
                  class="card-photo w-full h-full object-cover opacity-90 transition-all duration-700 pointer-events-none"
                />
                <!-- Photo overlay gradient -->
                <div class="card-overlay absolute inset-0 bg-gradient-to-t from-[#1A1530]/40 to-transparent opacity-0 transition-opacity duration-500 pointer-events-none"></div>
              </div>

              <!-- Caption area -->
              <p class="text-center text-[#8B7EAD] text-xs mt-3 font-medium tracking-wide pointer-events-none">{{ card.caption }}</p>

              <!-- Tiny heart accent -->
              <div class="card-heart absolute bottom-3 right-4 text-[#C2B5E8]/20 transition-colors duration-500 text-xs pointer-events-none">♡</div>
            </div>
          </div>

          <!-- BACK -->
          <div class="absolute inset-0 backface-hidden flip-back rounded-2xl" style="-webkit-backface-visibility: hidden; backface-visibility: hidden; transform: rotateY(180deg); -webkit-transform: rotateY(180deg);">
            <div class="w-full h-full bg-gradient-to-br from-[#C2B5E8] via-[#D4A8D0] to-[#E8A0BF] rounded-2xl flex items-center justify-center p-6 shadow-[0_12px_40px_rgba(194,181,232,0.25)] overflow-hidden">
              <div class="text-center pointer-events-none select-none">
                <span class="text-4xl mb-3 block drop-shadow-md">{{ card.emoji }}</span>
                <p class="text-[#1A1530] text-sm font-medium leading-relaxed">{{ card.backMessage }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

   
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface PolaroidCard {
  caption: string
  emoji: string
  backMessage: string
  image: string
  flipped: boolean
}

const polaroidCards = ref<PolaroidCard[]>([
  { caption: 'Namur', emoji: '💕', backMessage: 'Le meilleur souvenir de Vanbox je crois ahah', image: '/img/namur.jpeg', flipped: false },
  { caption: 'Nos 1 mois', emoji: '✨', backMessage: 'On était trop beau ! J\'étais tellement fier quand tu m\'as dit que je te connaissais mieux que personne en t\'offrant le carnet', image: '/img/1mois.jpeg', flipped: false },
  { caption: 'CE date', emoji: '🌸', backMessage: 'Tu étais si belle ce soir là. J\'aurais carrément pu aboyer pour toi ahah', image: '/img/red.jpeg', flipped: false },
  { caption: 'Les jardins éléctroniques', emoji: '💖', backMessage: '(Juste pour dire qu\'on doit écouter plus de musique tech ensemble)', image: '/img/jardin.jpeg', flipped: false },
  { caption: 'Paris à deux', emoji: '🦋', backMessage: 'Cette journée était sublime, on doit tellement aller ailleurs que Lille à deux. Ça nous fait tellement de bien. On était tropo heureux ce jour là', image: '/img/paris.jpeg', flipped: false },
  { caption: 'Le premier noêl ensemble', emoji: '🌙', backMessage: 'Il y en aura des dizaines d\'autres.', image: '/img/noel.jpeg', flipped: false },
  { caption: 'Ta première saint-Valentin (et la notre aussi)', emoji: '💫', backMessage: 'Je ferais tout pour te rendre aussi heureuse que ce jour-là', image: '/img/st.jpeg', flipped: false },
  { caption: 'Premier shooting photos', emoji: '🌹', backMessage: 'Mes photos dont je suis le plus fier, tu ressembles à un ange (même si ça me fane que tu les ai utilisé sur tinder ptdrrrrrrrrrrrrr + que tu m\'ai retiré de la collab azyyyy.).', image: '/img/ange.jpeg', flipped: false },
])

function flipCard(index: number) {
  polaroidCards.value[index].flipped = !polaroidCards.value[index].flipped
}
</script>

<style scoped>
.card-inner {
  transform-style: preserve-3d;
  -webkit-transform-style: preserve-3d;
  transition: transform 0.7s cubic-bezier(0.4, 0, 0.2, 1);
  transform: rotateY(0deg);
}

.card-inner.flip-active {
  transform: rotateY(180deg);
}

.backface-hidden {
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
}

.flip-back {
  transform: rotateY(180deg);
  -webkit-transform: rotateY(180deg);
}

@keyframes hover-float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-5px); }
}

.animate-hover-float {
  animation: hover-float 4s ease-in-out infinite;
}

.animate-hover-float:hover {
  animation-play-state: paused;
}

/* Hover effects scoped to devices that actually support pointer hover */
@media (hover: hover) and (pointer: fine) {
  .group:hover .card-photo {
    opacity: 1;
    transform: scale(1.08);
  }
  .group:hover .card-border {
    border-color: rgba(194, 181, 232, 0.2);
    box-shadow: 0 12px 40px rgba(194, 181, 232, 0.12);
  }
  .group:hover .card-overlay {
    opacity: 1;
  }
  .group:hover .card-heart {
    color: rgba(232, 160, 191, 0.4);
  }
}
</style>
