<template>
  <button
    type="submit"
  >
    Добавить товар
  </button>
</template>

<script>
export default {
  data () {
    return {
      allCorrect: false
    }
  }
}
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter&family=Source+Sans+Pro&display=swap');

$inactive-background: #EEEEEE;
$active-background: #7BAE73;
$inactive-color: #B4B4B4;
$active-color: #FFFFFF;
$font: 'Inter';

.new__submit {
  border: 0;
  margin-top: calc(24px - 16px);
  font-family: $font, Verdana, Geneva, Tahoma, sans-serif;
  text-align: center;
  font-size: 12px;
  transition: 0.5s linear all;
  width: 100%;
  padding: 10px 0px 11px 0px;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
}
.new__submit-active {
  background-color: $active-background;
  color: $active-color;
  cursor: pointer;
}
.new__submit-inactive {
  background-color: $inactive-background;
  color: $inactive-color;
}
</style>
