<template>
    <div class="btn-group mt-3">
        <PrimaryButton 
            class="btn"
            v-for="btn in filterButton" 
            :key="btn.name"
            :class="[filterName == btn.name ? 'btn-dark' : 'btn-outkine-dark']"
            @click="filtereHandler(btn.name)"    
        >
            {{ btn.title }}
        </PrimaryButton>
    </div>
</template>

<script>
export default {
    name: "Vue3SaAppFilter",
    props: {
        updateFiltereHandler: {
            type: Function,
            required: true
        },
        filterName: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            filterButton: [
                {
                    title: "Barcha kinolar",
                    name: "all",
                },
                {
                    title: "Mashhur  kinolar",
                    name: "popular",
                },
                {
                    title: "Eng ko'p ko'rilgan kinolar",
                    name: "mostViewers",
                },
            ],
            filter: "all",
        };
    },
    mounted() {
    },
    methods: {
        filtereHandler(filter) {
            this.filter = filter;
            this.updateFiltereHandler(this.filter);
        }
    },
};
</script>

<style>
.btn-group{
    border: 1px solid black;
}
</style>