<template>
  <div class="app-info">
    <p class="fs-3 text-uppercase">Barcha kinolar sonin: {{ allMuviesCount }}</p>
    <p class="fs-4 text-uppercase">Ko'rilgan  kinolar sonin: {{ FavouriteMuviesCount }}</p>
  </div>
</template>

<script>
export default {
  props:{
    allMuviesCount: {
        type: Date,
        required: true,
    },
    FavouriteMuviesCount: {
        type: Date,
        required: true,
    },
  }
}
</script>

<style>
.app-info{
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>