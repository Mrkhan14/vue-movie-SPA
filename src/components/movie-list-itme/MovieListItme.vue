<template>
    <li class="list-group-itme  d-flex justify-content-between">
        <span class="list-group-itme-label">Omar</span>

        <input type="number" class="list-group-itme-input" defaultValue="811">

        <div class="d-flex justify-content-center align-itmes-center">
            <button type="button" class="btn-cookie btn-sm">
                <i class="fas fa-cookie"></i>
            </button>

            <button type="button" class="btn-trash btn-sm">
                <i class="fas fa-trash"></i>
            </button>

            <i class="fas fa-star"></i>
        </div>
    </li>
</template>

<script>
export default {
    name: 'Vue3SaMovieListItme',

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
.list-group-itme{
    padding: 15px 20px;
    border-bottom: 1px solid #3d5a80;
}
.list-group-itme:last-child{
    border-bottom: none;
}
.list-group-itme span{
line-height: 35px;
font-size: 20px;
cursor: pointer;
width: 550px;
}

.list-group-itme input{
    line-height: 35px;
    font-size: 20px; 
    text-align: center;
    border: none;
    outline: none;
}
.list-group-itme button{
    width: 35px;
    height: 35px;
    margin: 3px;
    cursor: pointer;
    border: none;
    outline: none;

}
.list-group-itme .btn-cookie{
    color: #e09f3e;
}
.list-group-itme .btn-trash{
    color: #e5383b;
}
.list-group-itme .fa-star{
    width: 35px;
    height: 35px;
    text-align: center;
    line-height: 35px;
    font-size: 16px;
    color: #ffd700;
    transition: 0.3s all;
    transform:  translate(30px);
    opacity: 0;
}
.list-group-itme.link .fa-star{
    opacity: 1;
    transform: translateX(0);
}
.list-group-itme.favourite .list-group-itme-label,
.list-group-itme.favourite .list-group-itme-input
{
    color: #e09f3e;
}
</style>