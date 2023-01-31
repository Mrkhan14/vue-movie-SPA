<template>
    <ul class="movie-list list-grop">
       <movie-list-itme  v-for="(movie, index) in muviesYubor" :key="index"  :movieProps="movie"/>
    </ul>
</template>

<script>
import MovieListItme from '../movie-list-itme/MovieListItme.vue';
export default {
  components: { MovieListItme },
    name: 'Vue3SaMovieList',
    props: {
      muviesYubor: {
        type: Array,
        required: true
      }
    }
  };
</script>

<style  scoped>
.movie-list{
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>