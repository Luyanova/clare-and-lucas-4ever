<template>
  <section class="relative bg-[#0D0A1A] py-24 md:py-32 px-6 overflow-hidden">
    <!-- Background glow -->
    <div class="absolute bottom-0 left-1/4 w-[500px] h-[500px] bg-[#A0E8D0]/4 rounded-full blur-[140px] pointer-events-none"></div>

    <!-- Header -->
    <div class="text-center mb-16 md:mb-20 relative z-10">
      <span class="section-subtitle text-[#A0E8D0]/50 text-xs uppercase tracking-[0.3em] mb-4 block">on s'est pas dit tout ça pour rien chérie</span>
      <h2 class="section-title text-[#EDE8F5] text-4xl md:text-5xl lg:text-6xl">Quelques trucs qui nous reste à faire</h2>
      <div class="mt-6 mx-auto w-16 h-px bg-gradient-to-r from-transparent via-[#A0E8D0]/40 to-transparent"></div>
    </div>

    <!-- List -->
    <div class="max-w-xl mx-auto space-y-3 relative z-10">
      <div
        v-for="(item, index) in bucketList"
        :key="index"
        @click="toggleItem(index)"
        :class="[
          'group flex items-center gap-4 px-5 md:px-6 py-4 md:py-5 rounded-2xl cursor-pointer transition-all duration-500 border backdrop-blur-sm',
          item.checked
            ? 'bg-[#C2B5E8]/8 border-[#C2B5E8]/20 shadow-[0_0_30px_rgba(194,181,232,0.06)]'
            : 'bg-[#16112A]/60 border-[#C2B5E8]/6 hover:bg-[#1E1838]/80 hover:border-[#C2B5E8]/15'
        ]"
      >
        <!-- Custom checkbox -->
        <div
          :class="[
            'relative w-6 h-6 rounded-lg border-2 flex items-center justify-center flex-shrink-0 transition-all duration-500',
            item.checked
              ? 'bg-gradient-to-br from-[#C2B5E8] to-[#A098D0] border-[#C2B5E8] shadow-[0_0_16px_rgba(194,181,232,0.4)] scale-110'
              : 'border-[#5A4F78] group-hover:border-[#C2B5E8]/50'
          ]"
        >
          <svg
            v-if="item.checked"
            class="w-3.5 h-3.5 text-[#0D0A1A]"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            stroke-width="3"
          >
            <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
          </svg>
        </div>

        <!-- Text -->
        <span
          :class="[
            'text-sm md:text-base transition-all duration-500 select-none leading-relaxed',
            item.checked
              ? 'text-[#C2B5E8]/60 line-through decoration-[#C2B5E8]/30 decoration-2'
              : 'text-[#EDE8F5]/90'
          ]"
        >
          {{ item.text }}
        </span>

        <!-- Emoji -->
        <span
          :class="[
            'ml-auto text-lg transition-all duration-500 flex-shrink-0',
            item.checked ? 'opacity-100 scale-100' : 'opacity-0 scale-50'
          ]"
        >
          {{ item.emoji }}
        </span>
      </div>
    </div>

    <!-- Progress -->
    <div class="max-w-xl mx-auto mt-8 relative z-10">
      <div class="flex items-center justify-between mb-2">
        <span class="text-[#5A4F78] text-xs tracking-wide">Progression</span>
        <span class="text-[#C2B5E8]/70 text-xs font-medium">{{ checkedCount }} / {{ bucketList.length }}</span>
      </div>
      <div class="h-1 rounded-full bg-[#1E1838] overflow-hidden">
        <div
          class="h-full rounded-full bg-gradient-to-r from-[#C2B5E8] to-[#A0E8D0] transition-all duration-700 ease-out"
          :style="{ width: `${(checkedCount / bucketList.length) * 100}%` }"
        ></div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

interface BucketItem {
  text: string
  emoji: string
  checked: boolean
}

const bucketList = ref<BucketItem[]>([
  { text: 'Partir en voyage', emoji: '✈️', checked: false },
  { text: 'Enfin voir la mer ensemble', emoji: '🏖️', checked: false },
  { text: 'Adopter un chien', emoji: '🐩', checked: false },
  { text: 'Emménager ensemble à nouveau', emoji: '🏠', checked: false },
  { text: 'Être un couple de designer trop stylé', emoji: '🎨', checked: false },
  { text: 'Faire un nouveau shooting photo de toi', emoji: '📸', checked: false },
  { text: 'Aller au Kodz mdrrr', emoji: '🎵', checked: false },

])

function toggleItem(index: number) {
  bucketList.value[index].checked = !bucketList.value[index].checked
}

const checkedCount = computed(() => bucketList.value.filter((i) => i.checked).length)
</script>
