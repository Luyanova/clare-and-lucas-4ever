<template>
  <section class="relative bg-[#110E20] py-24 md:py-32 px-6 overflow-hidden">
    <!-- Background glow -->
    <div class="absolute top-1/2 right-0 w-[400px] h-[400px] bg-[#F0C4A0]/5 rounded-full blur-[120px] pointer-events-none -translate-y-1/2"></div>

    <!-- Header -->
    <div class="text-center mb-16 md:mb-20 relative z-10">
      <span class="section-subtitle text-[#F0C4A0]/50 text-xs uppercase tracking-[0.3em] mb-4 block">j'ai envie de t'embrasser à nouveau sur ce son</span>
      <h2 class="section-title text-[#EDE8F5] text-4xl md:text-5xl lg:text-6xl">Notre musique pour se kiss</h2>
      <div class="mt-6 mx-auto w-16 h-px bg-gradient-to-r from-transparent via-[#F0C4A0]/40 to-transparent"></div>
    </div>

    <!-- Player wrapper -->
    <div class="max-w-2xl mx-auto relative z-10">
      <div class="relative bg-[#16112A]/80 backdrop-blur-xl rounded-3xl border border-[#C2B5E8]/10 p-4 md:p-6 shadow-[0_8px_60px_rgba(0,0,0,0.4)] hover:border-[#C2B5E8]/20 transition-all duration-500">
        <!-- Top bar -->
        <div class="flex items-center gap-2.5 mb-5 px-1">
          <div class="w-2.5 h-2.5 rounded-full bg-[#E8A0BF]/60"></div>
          <div class="w-2.5 h-2.5 rounded-full bg-[#C2B5E8]/40"></div>
          <div class="w-2.5 h-2.5 rounded-full bg-[#F0C4A0]/30"></div>
          <div class="flex-1"></div>
          <span class="text-[#5A4F78] text-[10px] font-medium tracking-wider uppercase">now playing</span>
        </div>

        <!-- YouTube Embed -->
        <div class="relative w-full rounded-2xl overflow-hidden aspect-video bg-[#0D0A1A] ring-1 ring-white/5">
          <iframe
            :src="youtubeEmbedUrl"
            title="Notre Bande Originale"
            frameborder="0"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
            allowfullscreen
            class="absolute inset-0 w-full h-full"
          ></iframe>
        </div>

        <!-- Bottom equalizer -->
        <div class="flex items-end justify-center gap-[3px] mt-5 h-5">
          <span
            v-for="i in 20"
            :key="i"
            class="inline-block w-[3px] rounded-full bg-gradient-to-t from-[#C2B5E8]/30 to-[#E8A0BF]/30 animate-eq"
            :style="{
              height: `${4 + Math.sin(i * 0.7) * 10 + 6}px`,
              animationDelay: `${i * 0.08}s`,
              animationDuration: `${0.8 + Math.random() * 0.8}s`
            }"
          ></span>
        </div>
      </div>

      <!-- Ambient glow beneath -->
      <div class="w-2/3 mx-auto h-20 -mt-10 bg-[#C2B5E8]/5 rounded-full blur-[40px]"></div>
    </div>
  </section>
</template>

<script setup lang="ts">
const YOUTUBE_VIDEO_ID = '9_wLT8MXf_I'
const youtubeEmbedUrl = `https://www.youtube.com/embed/${YOUTUBE_VIDEO_ID}?rel=0&modestbranding=1`
</script>

<style scoped>
@keyframes eq {
  0%, 100% { transform: scaleY(0.3); }
  50% { transform: scaleY(1); }
}
.animate-eq {
  animation: eq 1s ease-in-out infinite;
  transform-origin: bottom;
}
</style>
