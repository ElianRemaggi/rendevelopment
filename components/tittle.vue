<script setup lang="ts">
import { computed } from 'vue'

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

// Computed property que usa la prop scrollValue
const shouldShowTitle = computed(() => {
    return props.scrollValue < 300
})

const shouldShowSubTitle = computed(() => {
    console.log(props.scrollValue)
    return props.scrollValue <= 300 && props.scrollValue >= 100 
})
</script>

<template>
    <div>
        <h1 id="title"
            class="text-5xl sm:text-6xl md:text-7xl lg:text-8xl xl:text-9xl text-center text-white font-bold py-16 mt-1 fixed top-70 left-0 w-full transition-opacity duration-300"
            :class="shouldShowTitle ? 'opacity-100' : 'opacity-0 pointer-events-none'">
            <u class="border-b-4 border-purple-500 pb-1">Rendevelopment</u>
        </h1>


        <h3 :class="shouldShowSubTitle ? 'opacity-100' : 'opacity-0 pointer-events-none'"
            class="m-auto text-2xl sm:text-3xl md:text-4xl lg:text-5xl xl:text-6xl text-center text-white font-bold py-16 mt-1 fixed top-120 left-0 w-full transition-opacity duration-300">
            Visualizando el futuro de tus proyectos inmobiliarios
        </h3>
    </div>
</template>

<style lang="scss" scoped></style>