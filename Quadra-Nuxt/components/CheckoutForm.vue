<script>
import axios from 'axios';


export default {
  data() {
    return {
      dadosCliente: {
        nome: '',
        endereco: '',
        cartao: '',
        expiracao: '',
        cvv: '',
        total: ""
      },
    
      compraProcessada: false
    };
  },
  method: {
    async processarCompra() {
      if (this.dadosCliente.nome && this.dadosCliente.endereco && this.dadosCliente.cartao && this.dadosCliente.expiracao && this.dadosCliente.cvv) {
        this.compraProcessada = true;
         await axios.post('http://10.60.44.36:3000/payment/create', {
          method: payment.method,
          total: payment.total,
          date: payment.date,
          iduser: payment.iduser,
          idlocation: payment.idlocation,
          cvv: payment.cvv, 
          numbercard: payment.numbercard, 
          dateexpiration: payment.dateexpiration, 
          address: payment.address,

    }) 
        
      }
    }
  }
};
</script>






<template>
  <div class="checkout-form">
    <h1 class="checkout-titulo">Finalizar Compra</h1>
    
    <form @submit.prevent="processarCompra">
      <div class="campo">
        <label for="nome">Nome Completo</label>
        <input type="text" v-model="dadosCliente.nome" required placeholder="Digite seu nome">
      </div>

      <div class="campo">
        <label for="endereco">Endereço</label>
        <input type="text" v-model="dadosCliente.endereco" required placeholder="Digite seu endereço">
      </div>

      <div class="campo">
        <label for="cartao">Número do Cartão</label>
        <input type="text" v-model="dadosCliente.cartao" required placeholder="Digite o número do seu cartão">
      </div>

      <div class="campo">
        <label for="expiracao">Data de Expiração</label>
        <input type="month" v-model="dadosCliente.expiracao" required>
      </div>

      <div class="campo">
        <label for="cvv">CVV</label>
        <input type="number" v-model="dadosCliente.cvv" required placeholder="CVV do cartão">
      </div>

      <div class="campo">
        <label for="total">Total</label>
        <input type="text" :value="total" disabled>
      </div>

      <button type="submit" class="checkout-botao">Confirmar Compra</button>
    </form>

    <div v-if="compraProcessada" class="sucesso">
      <h2>Compra Finalizada com Sucesso!</h2>
    </div>
  </div>
</template>



<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto+Mono:ital,wght@0,100..700;1,100..700&display=swap');

:root {
    --cor-background: rgb(31, 31, 31);
    --cor-navbar: rgb(24, 24, 24);
    --cor-principal: #c34de4;
    --cor-secundaria: #9d2baf;
}

body {
    margin: 0;
    background-color: var(--cor-background);
    font-family: "Roboto Mono", monospace;
    color: white;
}

.checkout-form {
    background-color: var(--cor-navbar);
    padding: 30px;
    border-radius: 10px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
    width: 100%;
    max-width: 600px;
    margin: 50px auto;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.checkout-titulo {
    font-size: 1.8rem;
    text-align: center;
    margin-bottom: 30px;
    color: var(--cor-principal);
}

.campo {
    width: 100%;
    margin-bottom: 20px;
}

.campo label {
    display: block;
    font-size: 1rem;
    margin-bottom: 5px;
}

.campo input {
    width: 100%;
    padding: 10px;
    font-size: 1rem;
    border: 1px solid #ccc;
    border-radius: 8px;
    background-color: #fff;
    color: var(--cor-background);
}

button.checkout-botao {
    padding: 12px 0;
    width: 100%;
    background-color: var(--cor-principal);
    color: white;
    font-size: 1.2rem;
    border: none;
    border-radius: 10px;
    cursor: pointer;
    transition: background-color 0.3s;
}

button.checkout-botao:hover {
    background-color: var(--cor-secundaria);
}

.sucesso {
    margin-top: 20px;
    background-color: #d4edda;
    padding: 10px;
    border: 1px solid #c3e6cb;
    border-radius: 4px;
    color: #155724;
    text-align: center;
}
</style>
