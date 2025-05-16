<script setup lang="ts">
import { inject } from 'vue';
import type { Ref } from 'vue';
import { computed } from 'vue';

const injectedScroll = inject<Ref<number>>('scrollValue', ref(0));

// Rango para la animación de entrada (4500-5500)
const ANIMATION_START = 4500;
const ANIMATION_END = 5500;

// Punto donde el contenido desaparece
const CONTENT_END = 6300;

// Calculamos el progreso de la animación (0 a 1)
const animationProgress = computed(() => {
    return Math.min(1, Math.max(0, (injectedScroll.value - ANIMATION_START) / (ANIMATION_END - ANIMATION_START)));
});

// Controlamos cuándo debe mostrarse el contenido (desde 4500 hasta 8000)
const shouldShowContent = computed(() => {
    return injectedScroll.value >= ANIMATION_START && injectedScroll.value <= CONTENT_END;
});

// Controlamos cuándo debe animarse (solo entre 4500-5500)
const shouldAnimate = computed(() => {
    return injectedScroll.value >= ANIMATION_START && injectedScroll.value <= ANIMATION_END;
});

const shouldRenderTittle = computed(() => {
    return injectedScroll.value >= ANIMATION_START && injectedScroll.value <= 5800;
})

const shouldRenderIdeas = computed(() => {
    return injectedScroll.value >= 5800 && injectedScroll.value <= 6200;
})

const shouldRenderPlus = computed(() => {
    return injectedScroll.value >= 6000 && injectedScroll.value <= 6200;
})

</script>

<template>
    <div :class="shouldShowContent ? 'opacity-100' : 'opacity-0 pointer-events-none'"
        class="fixed bottom-0 w-full h-screen transition-opacity duration-1000 bg-white">

        <!-- Barra de contenido (se desliza desde abajo) -->
        <div class="w-full absolute bottom-0 transition-transform duration-300 ease-out bg-white" :style="{
            transform: shouldAnimate ? `translateY(${(1 - animationProgress) * 100}%)` : 'translateY(0)',
            height: '70vh' /* Aumenté la altura para mejor distribución */
        }">
            <!-- Título - Reduje el padding superior -->
            <div :class="shouldRenderTittle ? 'opacity-100' : 'opacity-0 pointer-events-none'"
                class="text-4xl sm:text-5xl md:text-6xl text-center text-black font-bold pt-10 w-full transition-opacity duration-300 relative pb-4">
                <span class="relative inline-block text-black">
                    Impacta Visualmente tu
                    <span
                        class="text-transparent bg-clip-text bg-gradient-to-r from-purple-700 via-violet-600 to-cyan-500 font-bold drop-shadow-lg">
                        Proyecto
                    </span>
                    <span
                        class="absolute bottom-0 left-0 right-0 h-1 bg-gradient-to-r from-green-400 via-purple-400 to-purple-800"></span>
                </span>
            </div>

            <!-- Contenedor de iconos - Ajusté el margen y altura -->
            <div class="flex flex-col items-center justify-center px-4 h-[50vh]" style="margin-top: -25vh;">
                <div class="grid grid-cols-1 md:grid-cols-3 gap-0 max-w-6xl w-full items-center relative">
                    <!-- Panel izquierdo - Tus Ideas -->
                    <div :class="shouldRenderIdeas ? 'opacity-100' : 'opacity-0 pointer-events-none'"
                        class="relative bg-white p-6 rounded-2xl transition-all duration-500 shadow-sm col-span-1 w-full">
                        <div class="gradiantBorder py-1">
                            <h3 class="my-12 text-center font-bold text-2xl md:text-3xl mb-4 text-gray-800">Tus Ideas
                            </h3>
                            <div class="flex justify-center">
                                <img src="@/assets/idea.png" class="w-36 h-36 object-contain mb-16" alt="Icono de idea">
                            </div>
                        </div>
                    </div>

                    <!-- GIF del + en el centro -->
                    <div :class="shouldRenderPlus ? 'opacity-100' : 'opacity-0 pointer-events-none'"
                        class="flex items-center justify-center col-span-1 z-10">
                        <img src="@/assets/+.gif" class="w-24 h-24 object-contain" alt="Signo más animado">
                    </div>

                    <!-- Panel derecho - Nuestras Habilidades -->
                    <div :class="shouldRenderIdeas ? 'opacity-100' : 'opacity-0 pointer-events-none'"
                        class="relative bg-white p-6 rounded-2xl transition-all duration-500 shadow-sm col-span-1">
                        <div class="gradiantBorder py-1">
                            <h3 class="my-12 text-center font-bold text-2xl md:text-3xl mb-4 text-gray-800">Nuestras
                                Habilidades</h3>
                            <div class="flex justify-center space-x-4 ">
                                <img src="@/assets/arquitecta.png" class="w-36 h-36 object-contain"
                                    alt="Icono arquitectura">
                                <img src="@/assets/dev.png" class="w-36 h-36 object-contain mb-16"
                                    alt="Icono desarrollo">
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

</template>

<style scoped>
/* Animación adicional para suavizar la entrada */
.slide-up-enter-active {
    transition: all 0.5s ease-out;
}

.slide-up-enter-from {
    transform: translateY(100%);
}

.gradiantBorder {
    position: relative;
    border-radius: 16px;
    background-color: white;
    /* Para que coincida con tu rounded-2xl */
}

.gradiantBorder::before {
    content: '';
    position: absolute;
    top: -4px;
    left: -4px;
    right: -4px;
    bottom: -4px;
    border-radius: 18px;
    /* Un poco más grande que el contenedor para el borde */
    background: linear-gradient(90deg,
            #00ffff,
            /* cyan */
            #8a2be2,
            /* violeta */
            #9400d3,
            /* púrpura */
            #ff00ff
            /* rosa */
        );
    background-size: 400% 400%;
    z-index: -1;
    animation: gradientBorderAnimation 10s ease infinite;
}

@keyframes gradientBorderAnimation {
    0% {
        background-position: 0% 50%;
    }

    50% {
        background-position: 100% 50%;
    }

    100% {
        background-position: 0% 50%;
    }
}
</style>