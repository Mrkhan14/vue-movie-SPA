<template>
  <card-my>
    <p class="fs-3 text-uppercase">Barcha kinolar sonin: {{ allMuviesCount }}</p>
      <p class="fs-4 text-uppercase">Ko'rilgan  kinolar sonin: {{ FavouriteMuviesCount }}</p>
  </card-my>
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