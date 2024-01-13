<script setup>
import ChevronLeft from 'vue-material-design-icons/ChevronLeft.vue';
import movies from '../movies.json'
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
<div v-if="showFullVideo">
      <div @click="showFullVideo = false" class="absolute z-50 p-2 m-4 bg-white bg-opacity-50 rounded-full cursor-pointer">
        <ChevronLeft fillColor="#FFFFFF" :size="40"/>
      </div>
      <video 
        :src="'/videos/'+movie.name+'.mp4'" 
        autoplay 
        loop
        controls
        class="absolute z-0 w-[100vw] h-full object-fit"
      />
    </div>
</template>