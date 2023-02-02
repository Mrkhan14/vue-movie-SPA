<template>
    <div class="btn-group mt-3">
        <button 
            class="btn"   
            type="button"
            @click="filtereHandler('all')"
            :class="[filterName == 'all' ? 'btn-dark' : 'btn-outkine-dark']"
            >
            Barcha kinolar
        </button>
        <button 
            class="btn btn-outkine-dark" 
            type="button"
            @click="filtereHandler('popular')"
            :class="[filterName == 'popular' ? 'btn-dark' : 'btn-outkine-dark']"
            >
            Mashhur  kinolar
        </button>
        <button 
            class="btn btn-outkine-dark"
            type="button"
            @click="filtereHandler('mostViewers')"
             :class="[filterName == 'mostViewers' ? 'btn-dark' : 'btn-outkine-dark']"
            >
            Eng ko'p ko'rilgan kinolar
        </button>
    </div>
</template>

<script>
export default {
    name: 'Vue3SaAppFilter',
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
            filter: 'all',
        };
    },

    mounted() {
        
    },

    methods: {
        filtereHandler(filter){
            this.filter = filter
            this.updateFiltereHandler(this.filter)
        }
    },
};
</script>

<style>
.btn-group{
    border: 1px solid black;
}
</style>