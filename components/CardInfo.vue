<template>
  <div class="card__card-info">
    <p class="card__card-info__title">
      {{ title }}
    </p>
    <textarea
      :value="description"
      disabled
      class="card__card-info__desc"
    />
    <p class="card__card-info__cost">
      {{ cost }} руб.
    </p>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true
    },
    description: {
      type: String,
      required: false,
      default: null
    },
    cost: {
      type: Number,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
$font: #3F3F3F;
.card__card-info {
  flex-basis: 60%;
  display: flex;
  flex-direction: column;
  padding: 16px 16px 24px 16px;
}
.card__card-info > p {
  color: $font;
}
.card__card-info__title {
  font-weight: 600;
  font-size: 20px;
  margin-bottom: 16px;
}
.card__card-info__desc {
  font-size: 16px;
  margin-bottom: 32px;
  resize: none;
  border: 0;
  height: 80px;
}
.card__card-info__cost {
  font-weight: 600;
  font-size: 24px;
}
</style>
