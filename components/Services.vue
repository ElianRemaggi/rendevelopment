<script setup lang="ts">

// Definición de props con TypeScript
const props = defineProps({
    scrollValue: {
        type: Number,
        required: true,
        default: 0,
        validator: (value: number) => {
            return value >= 0
        }
    }
})


const ANIMATION_START = 1100 // Scroll donde comienza la animación
const ANIMATION_END = 2500   // Scroll donde termina la animación

const services = [
    {
        title: "Renderizados arquitectónicos 3D",
        description: "Imágenes fotorrealistas que muestran tus proyectos antes de construirlos",
        scrollValue: 1400
    },
    {
        title: "Tours virtuales interactivos",
        description: "Recorridos 360° que permiten explorar cada espacio",
        scrollValue: 1600
    },
    {
        title: "Maquetas digitales para pre-venta",
        description: "Modelos 3D interactivos para impulsar tus ventas",
        scrollValue: 1800
    },
    {
        title: "Visualizaciones para páginas web",
        description: "Integración perfecta de renderizados en tu sitio web",
        scrollValue: 2000
    }
]

const shouldRender = computed(() => {
    return props.scrollValue >= ANIMATION_START && props.scrollValue <= ANIMATION_END
})


</script>

<template>
    <div>
        <div :class="shouldRender ? 'opacity-100' : 'opacity-0 pointer-events-none fade-out'"
            class="fixed top-60 max-w-6xl min-w-full px-6 py-12">

            <div :class="shouldRender ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-5 fade-out'"
                class="absolute inset-0 bg-white/10 backdrop-blur-lg rounded-b-2xl border border-white/10 w-full transition-all duration-700 ease-out">
            </div>

            <div class="relative z-10">
                <h3 :class="props.scrollValue >= 1300 ? 'opacity-100' : 'opacity-0 pointer-events-none'"
                    class="text-3xl md:text-4xl font-bold text-center text-white mb-12">
                    Nuestros <span class="text-purple-300">Servicios</span>
                </h3>

                <ul class="grid grid-cols-1 md:grid-cols-2 gap-6 max-w-4xl mx-auto px-4">
                    <li v-for="(service, index) in services" :key="index"
                        :class="service.scrollValue <= props.scrollValue ? 'opacity-100' : 'opacity-0 pointer-events-none'"
                        class="group flex flex-col p-6 hover:bg-white/5 transition-all duration-300 rounded-xl">
                        <div
                            class="flex-shrink-0 p-3 bg-purple-500/20 rounded-lg group-hover:bg-purple-400/30 transition-all w-14 h-14 flex items-center justify-center mb-4">
                            <svg class="h-8 w-8 text-purple-300" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M5 13l4 4L19 7" />
                            </svg>
                        </div>
                        <div>
                            <h4 class="text-xl font-semibold text-white group-hover:text-purple-100 transition-colors">
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
    </div>
</template>

<style scoped>
.fade-out {
    opacity: 0;
    transition: opacity 0.5s ease-out;
}
</style>
