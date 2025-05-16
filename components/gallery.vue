<script setup lang="ts">
import { inject } from 'vue';
import type { Ref } from 'vue';
import { computed } from 'vue';

const injectedScroll = inject<Ref<number>>('scrollValue', ref(0));

const ANIMATION_START = 3000;
const ANIMATION_END = 4400;

import img1 from '@/assets/1.jpg';
import img2 from '@/assets/2.jpg';
import img3 from '@/assets/3.jpg';

const paths = [
    {
        path: img1,
        initialScrollValue: 3000,
        finalScrollValue: 3800,
        top: 0,
        justify: 'right-100',
        enterAnimation: 'fade-in-right'
    },
    {
        path: img2,
        initialScrollValue: 3200,
        finalScrollValue: 4000,
        top: 50,
        justify: '',
        enterAnimation: 'fade-in-up'
    },
    {
        path: img3,
        initialScrollValue: 3400,
        finalScrollValue: 4200,
        top: 100,
        justify: 'left-100',
        enterAnimation: 'fade-in-left'
    },
];

const shouldRender = computed(() => {
    return injectedScroll.value >= ANIMATION_START && injectedScroll.value <= ANIMATION_END
});
</script>

<template>
    <div :class="shouldRender ? 'opacity-100' : 'opacity-0 pointer-events-none'"
        class="fixed inset-0 w-full h-full transition-opacity duration-1000">

        <div v-for="(path, index) in paths" :key="index"
            :class="[
                'w-full h-1/3 fixed left-0 flex items-center justify-center',
                path.initialScrollValue > injectedScroll ? path.enterAnimation : '',
                path.finalScrollValue < injectedScroll ? 'exit-animation' : ''
            ]"
            :style="{ top: `${index * 33.33}%` }">

            <!-- Contenedor principal para marco e imagen -->
            <div :class="['relative transition-all duration-700 ease-[cubic-bezier(0.68,-0.6,0.32,1.6)]', 
                        path.justify.includes('right') ? 'mr-[100px]' : 
                        path.justify.includes('left') ? 'ml-[100px]' : '']"
                style="width: 33%; height: 80%;">

                <!-- Marco blurrado con animación -->
                <div :class="[
                    'absolute -inset-3 bg-white/10 backdrop-blur-lg rounded-2xl ',
                    'transition-all duration-500 delay-150',
                    shouldRender && path.initialScrollValue <= injectedScroll && path.finalScrollValue >= injectedScroll
                        ? 'opacity-100 scale-100'
                        : 'opacity-0 scale-90'
                ]">
                </div>

                <!-- Imagen con animación -->
                <div class="absolute inset-0 z-10 flex items-center justify-center">
                    <img :src="path.path" alt="Imagen" 
                        :class="[
                            'w-full h-full object-cover rounded-xl transition-all duration-500 ease-out',
                            'transform',
                            shouldRender && path.initialScrollValue <= injectedScroll && path.finalScrollValue >= injectedScroll
                                ? 'opacity-100 scale-95'
                                : 'opacity-0 scale-110'
                        ]"
                        :style="{ 'max-width': 'calc(100% - 16px)', 'max-height': 'calc(100% - 16px)' }" />
                </div>
            </div>
        </div>
    </div>
</template>

<style>
/* Animaciones de entrada */
.fade-in-right {
    animation: fadeInRight 0.7s ease-out forwards;
}

.fade-in-left {
    animation: fadeInLeft 0.7s ease-out forwards;
}

.fade-in-up {
    animation: fadeInUp 0.7s ease-out forwards;
}

/* Animación de salida */
.exit-animation {
    animation: exitAnimation 0.7s ease-in forwards;
}

/* Keyframes */
@keyframes fadeInRight {
    from {
        opacity: 0;
        transform: translateX(50px);
    }
    to {
        opacity: 1;
        transform: translateX(0);
    }
}

@keyframes fadeInLeft {
    from {
        opacity: 0;
        transform: translateX(-50px);
    }
    to {
        opacity: 1;
        transform: translateX(0);
    }
}

@keyframes fadeInUp {
    from {
        opacity: 0;
        transform: translateY(30px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

@keyframes exitAnimation {
    0% {
        opacity: 1;
        transform: translateY(0) scale(1);
    }
    50% {
        opacity: 0.8;
        transform: translateY(-20px) scale(0.95);
    }
    100% {
        opacity: 0;
        transform: translateY(30px) scale(0.9);
    }
}
</style>