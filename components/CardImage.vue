<template>
  <img :src="url" alt=":(">
</template>

<script>
export default {
  props: {
    url: {
      type: String,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
img {
  width: 100%;
  max-height: 200px;
  border-radius: 4px 4px 0px 0px;
}
</style>
