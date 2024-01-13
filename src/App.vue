<script setup>
import Navbar from '@/views/Navbar.vue';
import Carousel from '@/views/Carousel.vue';
import Video from '@/views/Video.vue';

import { useMovieStore } from './stores/movie'
import { storeToRefs } from 'pinia';
const useMovie = useMovieStore()
const {showFullVideo } = storeToRefs(useMovie)
</script>

<template>
  <div class="fixed w-full h-screen bg-black">

    <div v-if="!showFullVideo">
      <Navbar />
    </div>

    <Carousel />
    
    </div>

    <Video />

</template>
