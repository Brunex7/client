<template>
  <div class="tip-management">
    <div>

        <!-- Captura del monto total de propinas -->
        <div class="propinas">
            <label for="totalTips">Total de Propinas:</label>
            <input type="number" id="totalTips" v-model="totalTips" @input="updateRemaining">
        </div>
        
        <!-- Selección de la cantidad de empleados para dividir las propinas -->
    <div class="division">
        <label for="numEmployees">¿Entre cuántos quieres dividir las Propinas?</label>
        <select id="numEmployees" v-model="numEmployees">
            <option v-for="n in maxEmployees" :key="n">{{ n }}</option>
      </select>
    </div>

    <!-- Selección de la división de propinas -->
    <div class="divselec">
      <h4>División de Propinas</h4>
      <div>
          <input type="radio" id="equalSplit" value="equal" v-model="splitMethod">
          <label for="equalSplit">Equitativa</label>
          
          <input type="radio" id="customSplit" value="custom" v-model="splitMethod">
          <label class="person" for="customSplit">Personalizada</label>
      </div>
      
      <!-- Componente para la división personalizada -->
      <div v-if="splitMethod === 'custom'">
        <label for="customTips">Propinas por Empleado:</label>
        <div v-for="(employee, index) in employees" :key="index">
          <input type="number" v-model="customTips[index]" :placeholder="'Propinas para ' + employee.name">
        </div>
    </div>
</div>

<!-- Métodos de pago -->
<div class="conteM">
    <h3>Elige el Método de Pago</h3>
    <div class="boxbut">
        <button :class="{ active: paymentMethod === method }" v-for="method in paymentMethods" :key="method" @click="paymentMethod = method">{{ method }}</button>
    </div>
</div>
</div>


<div class="boxB">
    <!-- Registro de pagos -->
    <div class="payment-history">
        <h2>Historial de Pagos</h2>
        <ul>
          <li v-for="(payment, index) in paymentHistory" :key="index">{{ payment }}</li>
        </ul>
      </div>
      <div>

          <!-- Total pagado y restante por pagar -->
          <div class="textbox">
      <div class="textA">
        <h2>Total Pagado:</h2>
        <p>${{ totalPaid }}</p>
    </div>
    <div class="textB">
        <h2>Restante por Pagar:</h2>
        <p>${{ remainingToPay }}</p>
    </div>
    </div>

    <!-- Registro y documentación -->
    <div class="pagar">
        <button @click="payTips">Pagar Propinas</button>
    </div>
</div>
</div>
</div>
</template>

<script>
export default {
  data() {
    return {
      totalTips: 0,
      numEmployees: 1,
      splitMethod: '',
      paymentMethod: 'cash',
      paymentStatus: null,
      employees: [
        { id: 1, name: 'Empleado 1' },
        { id: 2, name: 'Empleado 2' },
        { id: 3, name: 'Empleado 3' },
        { id: 4, name: 'Empleado 4' },
        { id: 5, name: 'Empleado 5' },
        { id: 6, name: 'Empleado 6' },
      ],
      customTips: [],
      paymentHistory: []
    };
  },
  computed: {
    maxEmployees() {
      return this.employees.length;
    },
    totalPaid() {
      if (this.splitMethod === 'equal') {
        return (this.totalTips / this.numEmployees).toFixed(2);
      } else {
        return this.customTips.reduce((acc, curr) => acc + parseFloat(curr), 0).toFixed(2);
      }
    },
    remainingToPay() {
      return (this.totalTips - this.totalPaid).toFixed(2);
    },
    paymentMethods() {
      return ['cash', 'BBVA 123', 'Santander 123'];
    }
  },
  methods: {
    updateRemaining() {
      this.paymentStatus = null; // Limpiar el mensaje de confirmación al modificar el monto total de propinas
    },
    payTips() {
      let tipsToPay;
      if (this.splitMethod === 'equal') {
        tipsToPay = this.totalTips / this.numEmployees;
      } else {
        tipsToPay = this.customTips.reduce((acc, curr) => acc + curr, 0);
      }

      this.paymentHistory.push(`Pago de ${tipsToPay} propinas usando ${this.paymentMethod}.`);
      this.paymentStatus = `Se pagaron ${tipsToPay} propinas usando ${this.paymentMethod}.`;
    }
  }
};
</script>

<style scoped>
.tip-management {
  display: flex;
  justify-content: space-around;
}

.boxB {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.conteM {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.active {
  background-color: #ED6A5A;
  color: white;
}

.boxbut button {
  width: 194px;
  height: 100px;
  border-radius: 20px;
  font-weight: bold;
  border: 2px solid #C0C0C0;
  margin-left: 5px;
  box-shadow: 0 2px 6px 0 #C0C0C0;
}

.propinas label {
  font-size: medium;
  font-weight: bold;
  color: #ED6A5A;
  display: flex;
  left: 0;
}

.propinas input {
  font-weight: bold;
  color: #ED6A5A;
  background-color: #FBDEDA;
  padding: 15px;
  border-radius: 10px;
  font-size: xx-large;
  border: none;
  display: flex;
}

.division label {
  font-size: medium;
  font-weight: bold;
  display: flex;
  left: 0;
  margin-top: 50px;
}

.division select {
  font-size: medium;
  font-weight: bold;
  display: flex;
  left: 0;
  margin-top: 20px;
  height: 40px;
  width: 80px;
  border-radius: 10px;
}

.textbox {
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.textA {
  display: flex;
  align-items: center;
  width: 250px;
  justify-content: space-around;
  color: #ED6A5A;
}

.textB {
  display: flex;
  align-items: center;
  width: 350px;
  justify-content: space-around;
}

.divselec {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: flex-start;
  margin-bottom: 30px;
}

.pagar button {
  width: 100%;
  height: 70px;
  border-radius: 20px;
}

.payment-history {
    background-color: #F5F5F5;
    border: 2px solid #ED6A5A;
    border-radius: 20px;
    max-height: 200px; /* Altura máxima para la lista con desplazamiento */
    overflow-y: auto; /* Habilitar el desplazamiento vertical */
}
</style>
