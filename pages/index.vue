<template>
    <div class="bg-[#fdf5ff] w-screen h-screen flex justify-center items-center overflow-hidden relative">
        <div class="flex flex-col items-center justify-center gap-7">
            <div class="flex flex-col lg:flex-row items-center justify-center gap-10">
                <nuxt-img src="/img/polaUs2.png" alt="Pola Us" />
                <Logo class="w-50 h-50" />
            </div>
            <h1 class="text-[#02150E] text-2xl">Veux tu être ma Valentine ?</h1>

            <!-- Buttons -->
            <div class="flex items-center gap-6">
                <button
                    @click="handleOui"
                    class="px-8 py-3 rounded-full bg-[#f472b6] text-white font-semibold text-lg
                           shadow-[0_4px_14px_rgba(244,114,182,0.45)]
                           hover:scale-110 hover:shadow-[0_6px_20px_rgba(244,114,182,0.6)]
                           active:scale-95
                           transition-all duration-300 ease-out cursor-pointer"
                >
                    Oui
                </button>

                <button
                    ref="nonBtnRef"
                    @mouseover="teleportNon"
                    @click="teleportNon"
                    :style="nonBtnStyle"
                    :class="[
                        'px-8 py-3 rounded-full font-semibold text-lg transition-colors duration-200 cursor-pointer',
                        'border border-[#f9a8d4] text-[#d68fba] bg-[#fdf2f8]/60 hover:bg-[#fdf2f8]',
                        nonTeleported ? 'fixed z-50' : ''
                    ]"
                >
                    Non
                </button>
            </div>
        </div>

        <!-- Modal overlay -->
        <Transition name="modal">
            <div
                v-if="showModal"
                class="fixed inset-0 z-50 flex items-center justify-center bg-black/30 backdrop-blur-sm"
                @click.self="showModal = false"
            >
                <div class="bg-white rounded-2xl shadow-xl px-8 py-10 mx-4 max-w-md text-center
                            flex flex-col items-center gap-4 animate-bounce-in">
                    <span class="text-5xl">💖</span>
                    <p class="text-[#02150E] text-lg leading-relaxed">
                        Merci, j'ai hâte de faire cette première saint-valentin avec toi
                    </p>
                    <button
                        @click="showModal = false"
                        class="mt-2 px-6 py-2 rounded-full bg-[#f472b6] text-white font-medium
                               hover:scale-105 active:scale-95 transition-transform duration-200 cursor-pointer"
                    >
                        ❤️ Fermer
                    </button>
                </div>
            </div>
        </Transition>
    </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'
import confetti from 'canvas-confetti'

const showModal = ref(false)
const nonBtnRef = ref<HTMLButtonElement | null>(null)
const nonTeleported = ref(false)
const nonPosition = ref({ top: 0, left: 0 })

const nonBtnStyle = computed(() => {
    if (!nonTeleported.value) return {}
    return {
        top: `${nonPosition.value.top}px`,
        left: `${nonPosition.value.left}px`,
    }
})

function teleportNon() {
    nonTeleported.value = true
    const btnWidth = 120
    const btnHeight = 48
    const maxX = window.innerWidth - btnWidth
    const maxY = window.innerHeight - btnHeight
    nonPosition.value = {
        top: Math.random() * maxY,
        left: Math.random() * maxX,
    }
}

function launchHeartConfetti() {
    const heartShape = confetti.shapeFromPath({
        path: 'M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z',
    })

    const pinkShades = ['#ff69b4', '#ff85c8', '#f472b6', '#ec4899', '#db2777', '#fda4af', '#fb7185']

    const duration = 4000
    const end = Date.now() + duration

    function frame() {
        confetti({
            particleCount: 3,
            angle: 60,
            spread: 55,
            origin: { x: 0, y: -0.1 },
            colors: pinkShades,
            shapes: [heartShape],
            scalar: 1.4,
            gravity: 0.8,
            drift: 0.5,
            ticks: 300,
        })
        confetti({
            particleCount: 3,
            angle: 120,
            spread: 55,
            origin: { x: 1, y: -0.1 },
            colors: pinkShades,
            shapes: [heartShape],
            scalar: 1.4,
            gravity: 0.8,
            drift: -0.5,
            ticks: 300,
        })
        confetti({
            particleCount: 2,
            angle: 90,
            spread: 100,
            origin: { x: 0.5, y: -0.1 },
            colors: pinkShades,
            shapes: [heartShape],
            scalar: 1.2,
            gravity: 0.7,
            ticks: 300,
        })

        if (Date.now() < end) {
            requestAnimationFrame(frame)
        }
    }

    frame()
}

function handleOui() {
    showModal.value = true
    launchHeartConfetti()
}
</script>

<style scoped>
/* Modal transition */
.modal-enter-active,
.modal-leave-active {
    transition: opacity 0.3s ease;
}
.modal-enter-from,
.modal-leave-to {
    opacity: 0;
}

/* Bounce-in animation for modal content */
@keyframes bounce-in {
    0% {
        transform: scale(0.7);
        opacity: 0;
    }
    50% {
        transform: scale(1.05);
    }
    100% {
        transform: scale(1);
        opacity: 1;
    }
}
.animate-bounce-in {
    animation: bounce-in 0.4s ease-out;
}
</style>
