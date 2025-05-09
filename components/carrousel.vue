<script setup lang="ts">
import img1 from '@/assets/1.jpg';
import img2 from '@/assets/2.jpg';
import img3 from '@/assets/3.jpeg';
import img4 from '@/assets/4.jpg';

const paths = [img3, img2, img1, img4];
</script>

<template>
    <div class="m-auto w-full h-fit px-10 shadow-2xl rounded-b-3xl shadow-violet-500">
        <v-carousel class="my-16">
            <v-carousel-item v-for="(path, index) in paths" :key="index" :src="path" cover></v-carousel-item>
        </v-carousel>
    </div>
</template>