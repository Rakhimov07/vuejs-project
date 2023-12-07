<template>
    <ul class=" mt-5 list-group">
       <MovieItem v-for="movie in movies" :key="movie.id" @onTogle="$emit('onTogle',$event)" :movie="movie"  @onremove="$emit('onremove', $event)"/> 
    </ul>
</template>
<script>
import MovieItem from '../movie-item/movie-item.vue';
export default {
   components:{ MovieItem },
   props:{
      movies:{
         type:Array,
         required:true
      },
   }
}
</script>
<style>
    
</style>