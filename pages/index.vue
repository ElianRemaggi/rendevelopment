<script setup lang="ts">

import { useLenis } from 'lenis/vue'
import { ref, onMounted, onUnmounted, computed } from 'vue'

const scrollPosition = ref(0)
const lenis = useLenis()

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
        lenis.value.destroy()
    }
})

const services = [
    {
        title: "Renderizados arquitectónicos 3D",
        description: "Imágenes fotorrealistas que muestran tus proyectos antes de construirlos"
    },
    {
        title: "Tours virtuales interactivos",
        description: "Recorridos 360° que permiten explorar cada espacio"
    },
    {
        title: "Maquetas digitales para pre-venta",
        description: "Modelos 3D interactivos para impulsar tus ventas"
    },
    {
        title: "Visualizaciones para páginas web",
        description: "Integración perfecta de renderizados en tu sitio web"
    }
]

</script>

<template>

    <ScrollPosition />


    <div class="wrapper w-full pb-16 ">
        <div class="md:py-12 lg:py-16 xl:py-20">

            <h3
                class="m-auto text-2xl sm:text-3xl md:text-4xl lg:text-5xl xl:text-6xl text-center text-white font-bold py-16 mt-1">
                Visualizando el futuro de tus proyectos inmobiliarios
            </h3>

            <div class="w-full h-20 mt-16 pt-16 bg-cyan-100"></div>

            <div class="relative max-w-6xl min-w-full px-6 py-12">
                <!-- Fondo con efecto vidrio (glassmorphism) -->
                <div class="absolute inset-0 bg-white/10 backdrop-blur-lg rounded-b-2xl border border-white/10 w-full">
                </div>

                <div class="relative z-10">
                    <h3 class="text-3xl md:text-4xl font-bold text-center text-white mb-12">
                        Nuestros <span class="text-purple-300">Servicios</span>
                    </h3>

                    <ul class="grid grid-cols-1 md:grid-cols-2 gap-6 max-w-4xl mx-auto px-4">
                        <li v-for="(service, index) in services" :key="index"
                            class="group flex flex-col p-6 hover:bg-white/5 transition-all duration-300 rounded-xl">
                            <div
                                class="flex-shrink-0 p-3 bg-purple-500/20 rounded-lg group-hover:bg-purple-400/30 transition-all w-14 h-14 flex items-center justify-center mb-4">
                                <svg class="h-8 w-8 text-purple-300" fill="none" viewBox="0 0 24 24"
                                    stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                        d="M5 13l4 4L19 7" />
                                </svg>
                            </div>
                            <div>
                                <h4
                                    class="text-xl font-semibold text-white group-hover:text-purple-100 transition-colors">
                                    {{ service.title }}
                                </h4>
                                <p class="mt-2 text-purple-100/80 group-hover:text-purple-100 transition-colors">
                                    {{ service.description }}
                                </p>
                            </div>
                        </li>
                    </ul>
                </div>
            </div>

            <div class="flex justify-center ">

                <carrousel />

            </div>
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