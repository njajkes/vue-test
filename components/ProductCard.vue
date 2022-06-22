<template>
  <div class="card">
    <card-image
      :url="card.imglink"
    />
    <card-info
      :title="card.title"
      :description="card.description"
      :cost="card.cost"
    />
  </div>
</template>

<script>
import CardImage from './CardImage.vue'
import CardInfo from './CardInfo.vue'
export default {
  components: { CardInfo, CardImage },
  props: {
    card: {
      type: Object,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
$bgd-color: FFFEFB;

.card {
  margin-bottom: 16px;
  margin-left: 16px;
  border-radius: 4px;
  display: flex;
  flex-direction: column;
  width: 31%;
  background-color: $bgd-color;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  transition: cubic-bezier(0.075, 0.82, 0.165, 1) 0.5s all;
}
</style>
