<script setup>
import { inject } from 'vue';

const injectedScrollValue = inject('scrollValue');
const printScrollValue = () => {
    console.log('Scroll actual:', injectedScrollValue.value);
};
</script>

<template>
    <div class="fixed bottom-4 right-4 z-50 p-3 bg-black bg-opacity-70 text-white rounded-lg cursor-pointer"
        @click="printScrollValue">
        Scroll position: {{ injectedScrollValue }} px
    </div>
</template>