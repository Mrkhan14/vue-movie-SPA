<template>
    <ul class="movie-list list-grop">
       <movie-list-itme />
       <movie-list-itme />
       <movie-list-itme />
    </ul>
</template>

<script>
import MovieListItme from '../movie-list-itme/MovieListItme.vue';
export default {
  components: { MovieListItme },
    name: 'Vue3SaMovieList',

    data() {
        return {
            
        };
    },

    mounted() {
        
    },

    methods: {
        
    },
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