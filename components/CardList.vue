<template>
  <transition-group name="cards" tag="div" class="cards">
    <product-card
      v-for="card in cards"
      :key="card.id"
      :card="card"
      @deletecard="deleteCard"
    />
  </transition-group>
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
  },
  methods: {
    deleteCard (cardId) {
      this.$emit('deletecard', cardId)
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
.cards-move {
  transition: transform 1s;
}
</style>
