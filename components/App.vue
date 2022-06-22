<template>
  <div class="app">
    <div class="app__header">
      <p class="app__header__text">
        Добавление товара
      </p>
      <cards-switcher
        :option="sortOption"
        @switcherchange="orderChange"
      />
    </div>
    <div class="app__content">
      <new-form
        @create="pushNewCard"
      />
      <card-list
        :cards="cards"
        @deletecard="filterCards"
      />
    </div>
  </div>
</template>

<script>
import CardList from './CardList.vue'
import CardsSwitcher from './CardsSwitcher.vue'
import NewForm from './NewForm.vue'

export const sortOptions = {
  NAME: 0,
  TO_MAX: 1,
  TO_MIN: 2
}

export default {
  components: { CardsSwitcher, CardList, NewForm },
  data () {
    return {
      sortOption: sortOptions.NAME,
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
    },
    filterCards (cardId) {
      this.cards = this.cards.filter(card => card.id !== cardId)
    },
    orderChange (sortValue) {
      const condition = +sortValue
      const compareName = (a, b) => a.title?.toLowerCase()?.localeCompare(b.title.toLowerCase())
      const toMax = (a, b) => a.cost.split(' ').join('') - b.cost.split(' ').join('')
      const toMin = (a, b) => b.cost.split(' ').join('') - a.cost.split(' ').join('')

      switch (condition) {
        case sortOptions.NAME:
          this.cards = [...this.cards].sort(compareName)
          break
        case sortOptions.TO_MIN:
          this.cards = [...this.cards].sort(toMin)
          break
        case sortOptions.TO_MAX:
          this.cards = [...this.cards].sort(toMax)
          break
      }
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
