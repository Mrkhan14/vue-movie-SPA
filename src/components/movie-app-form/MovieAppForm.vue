<template>
    <card-my class="movie-app-form">
        <h3>Yangi kino qo'shish</h3>
        <form class="add-form d-flex" @submit.prevent>
            <InputMy class="new-movie-label" placeholder="Qanday kino?" v-model="name" />
            <InputMy class="new-movie-label" placeholder="Nechi Marotaba ko'rilgan" type="nunber" v-model="viewers" />
            <PrimaryButton class="btn btn-outline-dark" type="submit" @click="addMavie"> Qo'shmoq </PrimaryButton>
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
                // id: Date.now(),
            };
            this.$emit("creatMovie", newMavie);
            this.name = "",
                this.viewers = "";
        },
    },
};
</script>
