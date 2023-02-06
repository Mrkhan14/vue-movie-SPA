<template>
    <input 
        class="form-control search-input" 
        placeholder="Kinolarni qidirish" 
        v-model="term"
        @input="changeHandler"
    />
</template>

<script>
import input from '../../ui-components/input.vue';
export default {
    components: { input },
    name: 'Vue3SaSearchPanel',
    props: {
        updateTermHandler: {
            type: Function,
            required: true
        }
    },
    data() {
        return {
            term :'',
        };
    },
    methods: {
        changeHandler(e){
            this.term = e.target.value
            this.updateTermHandler(this.term)
        }
    }
};
</script>

<style  >
 .search-input{
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);

 }
</style>