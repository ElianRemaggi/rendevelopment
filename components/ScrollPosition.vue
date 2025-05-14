<script setup>
import { useLenis } from 'lenis/vue'
import { ref, onMounted, onUnmounted } from 'vue'

const scrollPosition = ref(0)
const lenis = useLenis()

// Función handler para el scroll
const scrollHandler = ({ scroll }) => {
    scrollPosition.value = Math.round(scroll)
}

onMounted(() => {
    // Usamos el método .on de la instancia lenis
    if (lenis.value) {
        lenis.value.on('scroll', scrollHandler)
    }
})

onUnmounted(() => {
    // Usamos el método .destroy para limpiar
    if (lenis.value) {
        lenis.value.destroy()
    }
})
</script>

<template>
    <div class="fixed bottom-4 right-4 z-50 p-3 bg-black bg-opacity-70 text-white rounded-lg">
        Scroll position: {{ scrollPosition }}px
    </div>
</template>