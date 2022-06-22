<template>
  <form
    class="new"
    @submit.prevent="addNewCard"
  >
    <new-input
      v-for="(inp) in formInputs"
      :key="inp.title"
      :name="inp.name"
      :title="inp.title"
      :placeholder="inp.placeholder"
      :req="inp.req"
      :type="inp.type"
      @formchange="formChange"
      @correctcheck="correctCheck"
      @inputerror="inputError"
      @inputpass="inputPass"
    />
    <new-submit
      :disabled="!allCorrect"
      :class="`new__submit ${allCorrect ? 'new__submit-active' : 'new__submit-inactive'}`"
    />
  </form>
</template>

<script>
import NewInput from './NewInput.vue'
import NewSubmit from './NewSubmit.vue'
export default {
  components: { NewInput, NewSubmit },
  data () {
    return {
      fields: {
        title: '',
        description: '',
        imglink: '',
        cost: 0
      },
      allCorrect: false,
      formInputs: [
        {
          name: 'title',
          title: 'Наименование товара',
          type: 'input',
          placeholder: 'Введите наименование товара',
          req: true
        },
        {
          name: 'description',
          title: 'Описание товара',
          type: 'textarea',
          placeholder: 'Введите описание товара',
          req: false
        },
        {
          name: 'imglink',
          title: 'Ссылка на изображение товара',
          type: 'url',
          placeholder: 'Введите ссылку',
          req: true
        },
        {
          name: 'cost',
          title: 'Цена товара',
          type: 'input',
          placeholder: 'Введите цену',
          req: true
        }
      ]
    }
  },
  computed: {
    correct () {
      return Object.fromEntries(this.formInputs.map(el => [el.name, !el.req]))
    }
  },
  methods: {
    addNewCard (event) {
      this.fields.id = Date.now()
      this.$emit('create', this.fields)
      this.fields = {
        title: '',
        description: '',
        imglink: '',
        cost: 0
      }
    },
    formChange (name, value) {
      this.fields[name] = value
    },
    correctCheck () {
      this.allCorrect = !(Object.values(this.correct).includes(false))
    },
    inputError (name) {
      this.correct[name] = false
      this.correctCheck()
    },
    inputPass (name) {
      this.correct[name] = true
      this.correctCheck()
    }
  }
}
</script>

<style lang="scss" scoped>
.new {
  flex-basis: 25%;
  min-width: 332px;
  background: #FFFEFB;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  padding: 24px;
  height: 440px;
}
</style>
