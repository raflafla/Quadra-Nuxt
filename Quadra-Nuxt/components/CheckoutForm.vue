<script setup>
  import axios from 'axios';
  // Usando 'ref' para quadraSelecionada
  let quadraSelecionada = ref(null);
  let data = ref(null);
  let horas = ref(null);

  // Usando onMounted para pegar os dados do localStorage corretamente
  onMounted(() => {
    const quadra = localStorage.getItem("quadraSelecionada");

    data.value = localStorage.getItem("data");

    if (quadra) {
      quadraSelecionada.value = JSON.parse(quadra);
    }
  });

  // Dados do cliente reativos
  const dadosCliente = reactive({
    nome: '',
    endereco: '',
    cartao: '',
    expiracao: '',
    cvv: '',
    total: 0
  });

  // Usando 'ref' para 'compraProcessada', que é um valor simples
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
      try {
        console.log("quadraSelecionada")
        console.log(quadraSelecionada)
        console.log(quadraSelecionada.value.id)
        console.log(data.value)
        let resposta= await axios.post('http://10.60.44.32:3000/location/create', {
          iduser: 1,
          idcourt: quadraSelecionada.value.id,
          date: data.value
        });

        await axios.put(`http://10.60.44.32:3000/quadra/update/${quadraSelecionada.value.id}`, {
          alugado: "Alugado"
        })

        // Enviando os dados para o servidor
        await axios.post('http://10.60.44.32:3000/payment/create', {
          method: dadosCliente.cartao,
          total: dadosCliente.total,
          date: new Date().toISOString(),
          iduser: 1,  // Substitua por um valor real
          idlocation: resposta.data.location_created.id,
          cvv: dadosCliente.cvv,
          numbercard: dadosCliente.cartao,
          dateexpiration: dadosCliente.expiracao,
          address: dadosCliente.endereco
        });
        compraProcessada.value = true; 
        window.location.href = "/perfil";

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
        <label>Nome Completo</label>
        <input type="text" v-model="dadosCliente.nome" required placeholder="Digite seu nome">
      </div>

      <div class="campo">
        <label>Endereço</label>
        <input type="text" v-model="dadosCliente.endereco" required placeholder="Digite seu endereço">
      </div>

      <div class="campo">
        <label>Número do Cartão</label>
        <input type="text" v-model="dadosCliente.cartao" required placeholder="Digite o número do seu cartão">
      </div>

      <div class="campo">
        <label>Data de Expiração</label>
        <input type="month" v-model="dadosCliente.expiracao" required>
      </div>

      <div class="campo">
        <label>CVV</label>
        <input type="number" v-model="dadosCliente.cvv" required placeholder="CVV do cartão">
      </div>

      <div class="campo">
        <label>Total</label>
        <input type="text" :value="quadraSelecionada?.preco || 0" disabled>
      </div>

      <button type="submit" class="checkout-botao">Confirmar Compra</button>
    </form>

    <div v-if="compraProcessada.value" class="sucesso">
      <h2>Compra Finalizada com Sucesso!</h2>
    </div>
  </div>
</template>

<style scoped>
@import url("../assets/pagamento.css");
</style>