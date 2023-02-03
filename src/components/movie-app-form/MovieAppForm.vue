<template>
    <card-my  class="movie-app-form">
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
            <PrimaryButton  class="btn btn-outline-dark" type="submit" @click="addMavie"> Qo'shmoq </PrimaryButton>
        </form>
    </card-my>
</template>

<script>
export default {
    data() {
        return {
            name: "",
            viewers: "",
        };
    },
    methods: {
        addMavie() {
            if (!this.name || !this.viewers)
                return;
            const newMavie = {
                name: this.name,
                viewers: this.viewers,
                favourite2: false,
                link: false,
                id: Date.now(),
            };
            this.$emit("creatMovie", newMavie);
            this.name = "",
                this.viewers = "";
        },
    }, 
};
</script>
