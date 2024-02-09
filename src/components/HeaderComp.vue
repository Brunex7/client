<template>
  <header class="box">
    <div class="containerA">
      <button @click="goBack">←<p>atras</p></button>
      <h1>Pago de Propinas</h1>
    </div>
    <div>
      <p class="text">Cantidad en Caja:</p>
      <div  class="price">
        <p>$5,000.00</p>
      </div>
    </div>
  </header>
  <hr/>
</template>

<script>
export default {
  methods: {
    goBack() {
      
    }
  }
};
</script>

<style scoped>
.box{
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: -20px;
}
.containerA{
  display: flex;
}
.containerA h1{
  margin-left: 30px;
}
.containerA button{
  display: flex;
  align-items: center;
  background-color: #fff;
  border: none;
  color: #ED6A5A;
  font-weight: bold;
}
.containerA button p{
  margin-left: 10px;
  font-weight: bold;
}
.price{
  margin-top: -30px;
}
.text{
  font-size: small;
  font-weight: bold;
  color: #ED6A5A;
  margin-left: 50px;
}

.price p{
  font-weight: bold;
  color: #ED6A5A;
  background-color: #FBDEDA;
  padding: 15px;
  border-radius: 10px;
  font-size: xx-large;
}
</style>
