<template>
  <select class="select">
    <option
      v-for="opt in optionlist"
      :key="opt.value"
      value="opt.value"
    >
      {{ opt.name }}
    </option>
  </select>
</template>

<script>
export default {
  data () {
    return {
      optionlist: [
        {
          value: 'name',
          name: 'По наименованию'
        },
        {
          value: 'toMax',
          name: 'Сначала дешёвые'
        },
        {
          value: 'toMin',
          name: 'Сначала дорогие'
        }
      ]
    }
  }
}
</script>

<style lang="scss" scoped>
.select {
  background: #FFFEFB;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  padding: 16px 10px 16px 11px;
  font-size: 12px;
  line-height: 15px;
  color: #B4B4B4;
  border: 0px;
}
.select > option {
  padding: 16px 10px 16px 11px;
}
</style>
