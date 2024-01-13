<script setup>
import movies from '../movies.json'
import VideoCarousel from '@/components/VideoCarousel.vue';
import MovieDetails from '@/components/MovieDetails.vue';
import { useMovieStore } from '../stores/movie'
import { onMounted, ref } from 'vue';
import { storeToRefs } from 'pinia';
const useMovie = useMovieStore()
const { movie, showFullVideo } = storeToRefs(useMovie)

let video = ref(null)

onMounted(() => {
  setTimeout(() => movie.value = movies[0][0], 100)
})
</script>

<template>
    <div v-if="!showFullVideo">
      <div class="fixed flex z-20 top-0 right-0 w-full h-[50%] bg-black pl-[120px] bg-clip-border">
        <div class="absolute z-30 h-[600px] left-[120px] w-[77%] right-0 top-0 bg-gradient-to-r from-black via-black" />
        
        <MovieDetails v-if="movie" :movie="movie" />

        <video 
          v-if="movie" 
          :src="'/videos/'+movie.name+'.mp4'" 
          autoplay 
          loop
          class="absolute z-0 h-[600px] right-0 top-0"
        />

      </div>

      <div class="fixed z-30 bottom-0 right-0 w-full h-[55%] pl-[120px] overflow-y-auto">
        <div class="fixed z-30 bottom-0 right-0 w-full h-[55%] pl-[120px] overflow-y-auto">
          <VideoCarousel class="pb-14 pt-14" category="Popular Movies" :movies="movies[0]" />
          <VideoCarousel class="pb-14" category="Horror Movies" :movies="movies[1]" />
          <VideoCarousel class="pb-32" category="Featured Movies" :movies="movies[2]" />
        </div>
      </div>
    </div>
</template>