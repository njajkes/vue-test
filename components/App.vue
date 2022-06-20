<template>
  <div class="app">
    <div class="app__header">
      <p class="app__header__text">
        Добавление товара
      </p>
      <cards-switcher />
    </div>
    <div class="app__content">
      <new-form />
      <card-list />
    </div>
  </div>
</template>

<script>
import CardList from './CardList.vue'
import CardsSwitcher from './CardsSwitcher.vue'
import NewForm from './NewForm.vue'
export default {
  components: { CardsSwitcher, CardList, NewForm }

}
</script>

<style lang="scss" scoped>
  $bgd-color: #FFFEFBCC;
  .app {
    padding: 32px;
    width: 100%;
    display: flex;
    flex-direction: column;
    background-color: $bgd-color;
  }
  .app > div {
    display: flex;
    flex-direction: row;
  }
  .app__header__text {
    font-weight: 600;
    font-size: 28px;
    line-height: 35px;
  }
  .app__header {
    display: flex;
    justify-content: space-between;
  }
</style>
