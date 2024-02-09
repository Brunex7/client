<template>
  <div>
    <label for="totalTips">Monto Total de Propinas:</label>
    <input type="number" id="totalTips" v-model="inputValue">
  </div>
</template>

<script>
export default {
  props: ['value'],
  data() {
    return {
      inputValue: this.value,
    };
  },
  watch: {
    inputValue(newValue) {
      this.$emit('input', newValue);
    },
  },
};
</script>
