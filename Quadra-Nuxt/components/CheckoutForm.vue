<script>
import axios from 'axios';
 
    let quadraSelecionada = ref(null);

     onMounted(()=>{
        quadraSelecionada.value = JSON.parse( localStorage.getItem("quadraSelecionada") )
      
    })

  const dadosCliente = ref({
        nome: '',
        endereco: '',
        cartao: '',
        expiracao: '',
        cvv: '',
        total: 0
      });
  const compraProcessada = ref(false);

  // Função para processar a compra
  const processarCompra = async () => {
    if (
      dadosCliente.nome &&
      dadosCliente.endereco &&
      dadosCliente.cartao &&
      dadosCliente.expiracao &&
      dadosCliente.cvv
    ) {
      compraProcessada.value = true;

      try {
        // Enviando os dados para o servidor
        await axios.post('http://10.60.44.36:3000/payment/create', {
          method: dadosCliente.cartao,  // Exemplo de como acessar os dados corretamente
          total: dadosCliente.total,
          date: new Date().toISOString(),  // Exemplo de como formatar a data
          iduser: 1,  // Substitua por um valor real
          idlocation: 1,  // Substitua por um valor real
          cvv: dadosCliente.cvv,
          numbercard: dadosCliente.cartao,
          dateexpiration: dadosCliente.expiracao,
          address: dadosCliente.endereco
        });

        // Aqui você pode definir algum feedback visual para o usuário.
      } catch (error) {
        console.error('Erro ao processar a compra:', error);
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
        <input type="text"  :value="quadraSelecionada.preco" disabled>
      </div>

      <button type="submit" class="checkout-botao">Confirmar Compra</button>
    </form>

    <div v-if="compraProcessada" class="sucesso">
      <h2>Compra Finalizada com Sucesso!</h2>
    </div>
  </div>
</template>



<style scoped>
@import url("../assets/pagamento.css");

</style>
