<template>
  <div>
    <button @click="payTips">Pagar Propinas</button>
    <div v-if="paymentStatus">
      <p>{{ paymentStatus }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['splitMethod', 'totalTips', 'numEmployees', 'customTips'],
  data() {
    return {
      paymentStatus: null,
    };
  },
  methods: {
    payTips() {
      let tipsToPay;
      if (this.splitMethod === 'equal') {
        tipsToPay = this.totalTips / this.numEmployees;
      } else {
        tipsToPay = this.customTips.reduce((acc, curr) => acc + curr, 0);
      }

      this.$emit('pay-tips', tipsToPay);
      this.paymentStatus = `Se pagaron ${tipsToPay} propinas usando ${this.paymentMethod}.`;
    },
  },
};
</script>
