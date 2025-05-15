<script setup lang="ts">
import { useLenis } from 'lenis/vue'
import { ref, onMounted, onUnmounted, provide } from 'vue'

const scrollPosition = ref(0)
const lenis = useLenis()

// ¡Provee la REF completa, no el .value!
provide('scrollValue', scrollPosition) // ← Cambio clave aquí

const scrollHandler = ({ scroll }: { scroll: number }) => {
    scrollPosition.value = Math.round(scroll)
}

onMounted(() => {
    if (lenis.value) {
        lenis.value.on('scroll', scrollHandler)
    }
})

onUnmounted(() => {
    if (lenis.value) {
        lenis.value.off('scroll', scrollHandler) // Cambia destroy() por off()
    }
})
</script>

<template>

    <ScrollPosition />


    <div class="wrapper w-full pb-16 ">
        <div class="md:py-12 lg:py-16 xl:py-20">
            <Tittle/>
            <services />
            <!--

            <div class="w-full h-20 mt-16 pt-16 bg-cyan-100"></div>

            

            <div class="flex justify-center ">

                <carrousel />

            </div>
    -->
        </div>

    </div>

    <div class="w-full h-20 mt-16 pt-16 h-min:2000px"></div>
</template>

<style scoped>
#tittle {
    margin-top: 10rem !important;
    text-shadow:
        0 2px 4px rgba(124, 58, 237, 0.5),
        0 4px 8px rgba(124, 58, 237, 0.3),
        0 8px 16px rgba(124, 58, 237, 0.2);
    transition: all 0.3s ease;
}

@media (max-width: 640px) {
    h1 {
        letter-spacing: -0.05em;
    }
}

@media (min-width: 1024px) {
    h1 {
        text-shadow:
            0 4px 8px rgba(124, 58, 237, 0.6),
            0 8px 16px rgba(124, 58, 237, 0.4),
            0 12px 24px rgba(124, 58, 237, 0.3);
    }
}
</style>