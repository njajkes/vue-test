<template>
  <div
    :class="`new-input${!isCorrect ? ' new-input__req-error_div' : ''}`"
  >
    <p
      :class="`new-input__name${req ? ' new-input__name-req' : ''}`"
    >
      {{ title }}
    </p>
    <textarea
      v-if="type === 'textarea'"
      :class="`new-input__area${!isCorrect ? ' new-input__req-error' : ''}`"
      :placeholder="placeholder"
      :value="value"
      @input="onChange"
    />
    <input
      v-else
      :type="type === 'input' ? 'text' : type"
      :class="`new-input__input${!isCorrect ? ' new-input__req-error' : ''}`"
      :placeholder="placeholder"
      :value="value"
      @focus="validationStart"
      @input="onChange"
      @blur="onBlur"
    >
  </div>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      required: true
    },
    type: {
      type: String,
      required: true
    },
    title: {
      type: String,
      required: true
    },
    req: Boolean,
    placeholder: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      isCorrect: true,
      value: ''
    }
  },
  methods: {
    validationStart (event) {
      if (!this.req) {
        this.isCorrect = true
      }
      if (this.req && !this.value) {
        this.isCorrect = true
      }
    },
    onChange (event) {
      if (this.name === 'cost') {
        this.value = event.target
          .value
          .replace(/[^\d]/g, '') // "12 2346" -> "122346"
          .replace(/\B(?=(?:\d{3})+(?!\d))/g, ' ') // "122346" -> "122 346"
      } else {
        this.value = event.target.value
      }
      this.$emit('formchange', this.name, this.value)
    },
    onBlur (event) {
      if (!this.req) {
        this.isCorrect = true
      } else if (this.req && !this.value) {
        this.isCorrect = false
        this.$emit('inputerror', this.name)
      } else {
        this.$emit('inputpass', this.name)
      }
    }
  }
}
</script>

<style lang="scss" scoped>
$gray: #B4B4B4;
$dark: #49485E;
$red: #FF8484;

.new-input {
  display: flex;
  position: relative;
  flex-direction: column;
  margin-bottom: 16px;
}
.new-input__name {
  position: relative;
  color: $dark;
  font-size: 10px;
  margin-bottom: 4px;
}
.new-input__name-req::after {
  content: url("data:image/svg+xml,%3Csvg width='4' height='4' viewBox='0 0 4 4' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Crect width='4' height='4' rx='2' fill='%23FF8484'/%3E%3C/svg%3E%0A");
  position: relative;
  top: -5px;
  width: 4px;
  height: 4px;
}
.new-input__input, .new-input__area {
  padding: 10px 16px 11px 16px;
  border: 0;
  background: #FFFEFB;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  font-size: 12px;
  color: $dark;
}
.new-input__input::placeholder, .new-input__area::placeholder {
  font-size: 12px;
  color: $gray;
}
.new-input__area {
  resize: none;
  min-height: 108px;
}
.new-input__req-error {
  border: 1px solid $red;
}
.new-input__req-error_div::after {
  top: calc(100% + 4px);
  position: absolute;
  font-size: 10px;
  color: $red;
  content: "Это поле является обязательным";
}
</style>
