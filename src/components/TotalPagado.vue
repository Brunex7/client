<template>
  <div>
    <h2>Total Pagado:</h2>
    <p>{{ totalPaid }}</p>
  </div>
</template>

<script>
export default {
  props: ['totalPaid'],
};
</script>