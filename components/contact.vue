<script setup lang="ts">
import { inject } from 'vue';
import type { Ref } from 'vue';
import { computed } from 'vue';

const injectedScroll = inject<Ref<number>>('scrollValue', ref(0));

const ANIMATION_START = 6200;
const ANIMATION_END = 7100;

const shouldRender = computed(() => {
    return injectedScroll.value >= ANIMATION_START && injectedScroll.value <= ANIMATION_END;
})

const resetScroll = () => {
    injectedScroll.value = 0;
    window.scrollTo({ top: 0, behavior: 'smooth' });
}
</script>

<template>
    <div :class="shouldRender ? 'opacity-100' : 'opacity-0 pointer-events-none'"
         class="fixed inset-0 rounded-3xl w-3/4 h-3/4 transition-opacity duration-1000 bg-black bg-opacity-70 flex flex-col items-center justify-center mx-auto my-auto left-0 right-0 top-0 bottom-0">

        <!-- Texto de contacto con gradiente -->
        <div class="text-center mb-8">
            <h2 class="text-5xl font-bold mb-4 bg-clip-text text-transparent bg-gradient-to-r from-cyan-400 via-purple-400 to-pink-500">
                Contáctanos
            </h2>
            <a href="mailto:info@tudominio.com"
               class="text-3xl font-medium text-cyan-200 hover:text-white transition-colors duration-300 underline underline-offset-8 decoration-cyan-400/50">
                info@rendevelopment.com
            </a>
        </div>

        <!-- Contenedor del GIF centrado -->
        <div class="relative w-3/4 h-1/2 flex items-center justify-center">
            <img src="@/assets/contact.gif" class="max-w-full max-h-full object-contain" alt="Animación de contacto"
                 style="filter: drop-shadow(0 0 10px rgba(255, 255, 255, 0.5));">
        </div>

        <!-- Botón Volver al inicio -->
        <button @click="resetScroll"
                class="mt-8 px-8 py-3 rounded-full bg-gradient-to-r from-purple-600 to-cyan-500 text-white font-bold hover:from-purple-500 hover:to-cyan-400 transition-all duration-300 shadow-lg hover:shadow-cyan-500/30 flex items-center gap-2">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 10l7-7m0 0l7 7m-7-7v18" />
            </svg>
            Volver al inicio
        </button>
    </div>
</template>

<style scoped></style>