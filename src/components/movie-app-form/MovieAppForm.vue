<template>
    <div class="movie-app-form">
       <h3>Yangi kino qo'shish</h3>
       <form class="add-form d-flex" @submit.prevent>
            <input 
                type="text" 
                class="form-control new-movie-label" 
                placeholder="Qanday kino?"
                :value="name"
                @input="name = $event.target.value"
            >
            <input 
                type="text" 
                class="form-control new-movie-label" 
                placeholder="Nechi Marotaba ko'rilgan"
                :value="viewers"
                @input="viewers = $event.target.value"
                >
            <button class="btn btn-outline-dark" type="submit" @click="addMavie"> Qo'shmoq</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'Vue3SaMovieAppForm',

    data() {
        return {
            name: '',
            viewers:'',
        };
    },

    // mounted() {
        
    // },

    methods: {
        addMavie(){
            const newMavie ={
                name: this.name,
                viewers: this.viewers,
                favourite2: false,
                link: false,
                id: Date.now(),
            }
            this.$emit('creatMovie', newMavie)
            this.name= "",
            this.viewers= ""
        },
    },
};
</script>

<style scoped>
.movie-app-form{
    margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>