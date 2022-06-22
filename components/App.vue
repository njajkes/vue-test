<template>
  <div class="app">
    <div class="app__header">
      <p class="app__header__text">
        Добавление товара
      </p>
      <cards-switcher />
    </div>
    <div class="app__content">
      <new-form @create="pushNewCard" />
      <card-list :cards="cards" />
    </div>
  </div>
</template>

<script>
import CardList from './CardList.vue'
import CardsSwitcher from './CardsSwitcher.vue'
import NewForm from './NewForm.vue'

export default {
  components: { CardsSwitcher, CardList, NewForm },
  data () {
    return {
      cards: []
    }
  },
  mounted () {
    this.cards = JSON.parse(localStorage.getItem('cards'))
    if (typeof window !== 'undefined') {
      window.addEventListener('beforeunload', (e) => {
        localStorage.setItem('cards', JSON.stringify(this.cards))
      })
    }
  },
  methods: {
    pushNewCard (card) {
      this.cards.push(card)
    }
  }
}
</script>

<style lang="scss" scoped>
$bgd-color: #FFFEFBCC;
.app {
  padding: 32px;
  width: 100%;
  min-height: 100vh;
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
  margin-bottom: 16px;
}
</style>
