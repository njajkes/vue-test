<template>
  <div class="cards">
    <product-card
      v-for="card in cards"
      :key="card.id"
      :card="card"
    />
  </div>
</template>

<script>
import ProductCard from './ProductCard.vue'
export default {
  components: { ProductCard },
  props: {
    cards: {
      type: Array,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
.cards {
  flex-basis: 75%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-around;
}
</style>
