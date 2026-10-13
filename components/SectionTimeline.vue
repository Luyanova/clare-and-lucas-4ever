<template>
  <section class="relative bg-[#0D0A1A] py-24 md:py-32 px-6 overflow-hidden">
    <!-- Background glow orbs -->
    <div class="absolute top-20 -left-32 w-96 h-96 bg-[#C2B5E8]/8 rounded-full blur-[120px] pointer-events-none"></div>
    <div class="absolute bottom-20 -right-32 w-80 h-80 bg-[#E8A0BF]/6 rounded-full blur-[100px] pointer-events-none"></div>

    <!-- Header -->
    <div class="text-center mb-20 md:mb-28 relative z-10">
      <span class="section-subtitle text-[#C2B5E8]/60 text-xs uppercase tracking-[0.3em] mb-4 block">une petite timeline toute mimi</span>
      <h2 class="section-title text-[#EDE8F5] text-4xl md:text-5xl lg:text-6xl">Nous deux</h2>
      <div class="mt-6 mx-auto w-16 h-px bg-gradient-to-r from-transparent via-[#C2B5E8]/50 to-transparent"></div>
    </div>

    <!-- Timeline -->
    <div class="relative max-w-4xl mx-auto">
      <!-- Continuous vertical line -->
      <div class="absolute left-8 md:left-1/2 top-0 bottom-0 md:-translate-x-px">
        <div class="w-px h-full bg-gradient-to-b from-transparent via-[#C2B5E8]/25 to-transparent"></div>
        <!-- Animated glow on the line -->
        <div class="absolute inset-0 w-px bg-gradient-to-b from-transparent via-[#C2B5E8]/60 to-transparent animate-line-glow"></div>
      </div>

      <!-- Steps -->
      <div
        v-for="(step, index) in timelineSteps"
        :key="index"
        :ref="(el) => setStepRef(el as HTMLElement, index)"
        :class="[
          'relative mb-20 md:mb-28 last:mb-0 transition-all duration-1000 ease-[cubic-bezier(0.16,1,0.3,1)]',
          stepVisible[index] ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-16',
        ]"
        :style="{ transitionDelay: `${index * 100}ms` }"
      >
        <!-- Dot -->
        <div class="absolute left-8 md:left-1/2 -translate-x-1/2 z-20 flex items-center justify-center">
          <div class="w-3 h-3 rounded-full bg-[#C2B5E8] shadow-[0_0_20px_rgba(194,181,232,0.6)]"></div>
          <div class="absolute w-7 h-7 rounded-full border border-[#C2B5E8]/20 animate-ping-slow"></div>
        </div>

        <!-- Card -->
        <div
          :class="[
            'ml-20 md:ml-0 md:w-[calc(50%-3rem)]',
            index % 2 === 0 ? 'md:mr-auto' : 'md:ml-auto'
          ]"
        >
          <div class="group relative bg-[#16112A]/80 backdrop-blur-xl rounded-2xl border border-[#C2B5E8]/10 p-6 hover:border-[#C2B5E8]/25 transition-all duration-500 hover:shadow-[0_8px_40px_rgba(194,181,232,0.08)]">
            <!-- Date chip -->
            <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-[#C2B5E8]/10 border border-[#C2B5E8]/15 mb-4">
              <div class="w-1.5 h-1.5 rounded-full bg-[#C2B5E8]"></div>
              <span class="text-[#C2B5E8] text-xs font-medium tracking-wide">{{ step.date }}</span>
            </div>

            <!-- Image -->
            <div class="relative rounded-xl overflow-hidden mb-4 aspect-[16/10] bg-[#1E1838]">
              <nuxt-img :src="step.image" :alt="step.title" class="w-full h-full object-cover opacity-80 group-hover:opacity-100 group-hover:scale-105 transition-all duration-700" />
              <div class="absolute inset-0 bg-gradient-to-t from-[#0D0A1A]/60 via-transparent to-transparent"></div>
            </div>

            <!-- Text -->
            <h3 class="text-[#EDE8F5] font-semibold text-lg mb-2">{{ step.title }}</h3>
            <p class="text-[#8B7EAD] text-sm leading-relaxed">{{ step.description }}</p>

            <!-- Corner accent -->
            <div class="absolute -top-px -right-px w-12 h-12 overflow-hidden rounded-tr-2xl">
              <div class="absolute top-0 right-0 w-16 h-16 bg-gradient-to-bl from-[#C2B5E8]/10 to-transparent"></div>
            </div>
          </div>

          <!-- Connector arm (desktop) -->
          <div
            :class="[
              'hidden md:block absolute top-5 w-8 h-px bg-[#C2B5E8]/15',
              index % 2 === 0 ? 'right-[calc(50%-3rem+1px)]' : 'left-[calc(50%-3rem+1px)]'
            ]"
          ></div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

interface TimelineStep {
  date: string
  title: string
  description: string
  image: string
}

const timelineSteps: TimelineStep[] = [
  {
    date: '18 mai 2025',
    title: 'Les débuts à solfé',
    description: 'Alalala, tout à commencé prêt de ton ancien appartement, d\'abord à parler des heures dans la voiture, puis en s\'appelant tout le temps, je n\'ai jamais ressenti une connexion aussi forte avec quelqu\'un',
    image: '/img/timeline1.jpeg',
  },
  {
    date: '23 mai 2025',
    title: 'Déjà ?!?!',
    description: 'C\'est encore à l\'époque où je venais te cherchais à Euratech qu\'un soir comme un gros débile je t\ai proposé de sortir avec moi, et ça a marché youpi, alors que l\'appart était vide, tu le remplissais de bonheur à chaque fois que tu venais',
    image: '/img/timeline2.jpg',
  },
  {
    date: '18 août 2025',
    title: 'L\'appart à deux',
    description: 'J\' ai vraiment été chiant avec toi des fois, je suis désolé mais vivre avec toi a été l\'une des expériences les plus douces de ma vie, te revoir tout les soirs était si réconfortant, je me sentais combler même si je te le disais pas assez.',
    image: '/img/timeline3.jpeg',
  },
  {
    date: '22 mai 2026',
    title: 'Nos 1 an',
    description: 'Malgré toutes les difficultés qu\'on a traversé, on est toujours la l\'un pour l\'autre, on a réussi à tenir jusqu\'a nos un an et je t\'aime de plus en plus chaque jour, j\'ai besoin de te savoir heureuse.',
    image: '/img/timeline4.jpeg',
  },
  {
    date: '11 Octobre 2026',
    title: 'Se remettre ensemble ???',
    description: 'C\'est fou, quoi qu\'il nous arrive on finit toujours par se retrouver et à passer des moments ensemble qu\'on ne peut pas vivre avec d\'autres personnes. Tu es tellement spéciale pour moi, on a vécu le pire et le meilleur ensemble. Pourtant rien ne nous as vraiment éloigné. ',
    image: '/img/timeline5.jpeg',
  },
]

const stepRefs = ref<(HTMLElement | null)[]>([])
const stepVisible = ref<boolean[]>(timelineSteps.map(() => false))
let observer: IntersectionObserver | null = null

function setStepRef(el: HTMLElement | null, index: number) {
  if (el) stepRefs.value[index] = el
}

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        const idx = stepRefs.value.indexOf(entry.target as HTMLElement)
        if (idx !== -1 && entry.isIntersecting) {
          stepVisible.value[idx] = true
        }
      })
    },
    { threshold: 0.1, rootMargin: '0px 0px -60px 0px' }
  )
  stepRefs.value.forEach((el) => {
    if (el) observer!.observe(el)
  })
})

onUnmounted(() => {
  observer?.disconnect()
})
</script>

<style scoped>
@keyframes line-glow {
  0%, 100% { opacity: 0; transform: translateY(-100%); }
  50% { opacity: 1; }
  100% { transform: translateY(100%); }
}
.animate-line-glow {
  animation: line-glow 6s ease-in-out infinite;
}

@keyframes ping-slow {
  0% { transform: scale(1); opacity: 0.5; }
  75%, 100% { transform: scale(2); opacity: 0; }
}
.animate-ping-slow {
  animation: ping-slow 3s cubic-bezier(0, 0, 0.2, 1) infinite;
}
</style>
