<script setup lang="ts">
import { inject, computed } from 'vue'
import type { Ref } from 'vue'
import { gsap } from 'gsap'

const injectedScrollValue = inject<Ref<number>>('scrollValue', ref(0));

// Computed property que usa la prop scrollValue
const shouldShowTitle = computed(() => {
    return injectedScrollValue.value >= 0 && injectedScrollValue.value <= 1000
})

const shouldShowSubTitle = computed(() => {
    return injectedScrollValue.value >= 100 && injectedScrollValue.value <= 1000
})


const subtitle = ref('Visualizando el futuro de tus proyectos inmobiliarios')
const displayedText = ref('')
const subtitleRef = ref<HTMLElement | null>(null)

const ANIMATION_START = 100 // Scroll donde comienza la animación
const ANIMATION_END = 750   // Scroll donde termina la animación
const ANIMATION_DURATION = ANIMATION_END - ANIMATION_START

const animationProgress = computed(() => {
    return Math.min(1, Math.max(0, (injectedScrollValue.value - ANIMATION_START) / ANIMATION_DURATION));
})

watch(animationProgress, (progress) => {
    const charsToShow = Math.floor(progress * subtitle.value.length)
    displayedText.value = subtitle.value.substring(0, charsToShow)

    // Animación de letras individuales
    if (subtitleRef.value) {
        const chars = subtitleRef.value.querySelectorAll('.char')
        gsap.to(chars, {
            opacity: 1,
            x: 0,
            duration: 0.3,
            stagger: 0.03,
            ease: 'power2.out'
        })
    }
})

// Prepara las letras al montar el componente
onMounted(() => {
    if (subtitleRef.value) {
        gsap.set(subtitleRef.value.querySelectorAll('.char'), {
            opacity: 0,
            x: -10
        })
    }
})


</script>

<template>
    <div>
        <h1 id="title" :class="shouldShowTitle ? 'opacity-100' : 'opacity-0 pointer-events-none'"
            class="text-5xl sm:text-6xl md:text-7xl lg:text-8xl xl:text-9xl text-center text-white font-bold py-16 mt-1 fixed top-70 left-0 w-full transition-opacity duration-300">
            <u :class="shouldShowTitle ? 'opacity-100' : 'opacity-0 pointer-events-none'"
                class="border-b-4 border-purple-500 pb-1">Rendevelopment</u>
        </h1>

        <h3 id="subtitle" :class="shouldShowSubTitle ? 'opacity-100' : 'opacity-0 pointer-events-none'"
            class="m-auto text-2xl sm:text-3xl md:text-4xl lg:text-5xl xl:text-6xl text-center text-white font-bold py-16 mt-1 fixed top-120 left-0 w-full transition-opacity duration-300">
            {{ displayedText }}
        </h3>
    </div>
</template>

<style lang="scss" scoped></style>