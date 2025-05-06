<script setup lang="ts">

const paths = [
    '@/assets/1.jpg',
    '@/assets/2.jpg',
    '@/assets/3.jpeg',
    '@/assets/4.jpg'
]
</script>

<template>
    <div class="m-auto my-40 w-3/4 h-fit p-10 shadow-2xl rounded-3xl">
        <v-carousel>
            <v-carousel-item src="https://cdn.vuetifyjs.com/images/cards/docks.jpg" cover></v-carousel-item>

            <v-carousel-item src="https://cdn.vuetifyjs.com/images/cards/hotel.jpg" cover></v-carousel-item>

            <v-carousel-item src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg" cover></v-carousel-item>
        </v-carousel>
    </div>




    <div class="m-auto my-40 w-3/4 h-fit p-10 shadow-2xl rounded-3xl">
        <v-carousel>
            <v-carousel-item v-for="path in paths" :src="path" cover></v-carousel-item>
        </v-carousel>
    </div>

</template>


<style scoped></style>