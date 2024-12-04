<script setup>
  import axios from 'axios';

  // Inicializando como null para evitar acessar undefined
  let quadraSelecionada = ref(null);
  let userselecionado = ref(null)
  let data = ref(null);
  let horas = ref(null);

  // onMounted: Carregar quadra e data do localStorage
  onMounted(() => {
    const quadra = localStorage.getItem("quadraSelecionada");
    const user = localStorage.getItem("user")
    data.value = localStorage.getItem("data");
   if (user) {
      userselecionado.value = JSON.parse(user);
    }

    if (quadra) {
      quadraSelecionada.value = JSON.parse(quadra);
    }
  });

  const dadosCliente = reactive({
    nome: '',
    endereco: '',
    cartao: '',
    expiracao: '',
    cvv: '',
    total: 0
  });

  const compraProcessada = ref(false);

  const processarCompra = async () => {
    
  
    if (
      dadosCliente.nome &&
      dadosCliente.cartao &&
      dadosCliente.expiracaoMes &&
      dadosCliente.expiracaoAno &&
      dadosCliente.cvv
      
    ) { 
      try {
        // Verificar se quadraSelecionada está disponível
        if (!quadraSelecionada.value || !quadraSelecionada.value.id) {
          console.error('Quadra não selecionada corretamente');
          return;
        }
        console.log("location  criando")
        // Criar a reserva de quadra
        let resposta = await axios.post('http://10.60.44.32:3001/location/create', {
          iduser: userselecionado.value.id,
          idcourt: quadraSelecionada.value.id,
          date: data.value
        });
        console.log("quadra atualizando")
        // Atualizar a quadra como 'alugada'
        await axios.put(`http://10.60.44.32:3001/quadra/update/${quadraSelecionada.value.id}`, {
          alugado: "Alugado"
        });
  
        const date = new Date();

        const formattedDate = date.toISOString().split('T')[0];
        console.log(formattedDate);

        let preco = quadraSelecionada.value.preco; // Exemplo: "R$ 100,50"

        // Remover o símbolo "R$" e substituir a vírgula por ponto
        let precoDecimal = parseFloat(preco.replace("R$", "").replace(",", ".").trim());

        await axios.post('http://10.60.44.32:3001/payment/create', {
          total: precoDecimal,
          date: formattedDate,
          iduser: userselecionado.value.id,
          idlocation: resposta.data.location_created.id,
          cvv: dadosCliente.cvv,
          numbercard: dadosCliente.cartao,
          yearcard: dadosCliente.expiracaoMes,
          monthcard: dadosCliente.expiracaoAno
        });
       
        compraProcessada.value = true;
        window.location.href = "/perfil";

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
        <label>Número do Cartão</label>
        <input type="text" v-model="dadosCliente.cartao" required placeholder="Digite o número do seu cartão">
      </div>

      <div class="campo">
        <label>Data de Expiração</label>
        <div class="campo-expiracao">
          <input type="text" v-model="dadosCliente.expiracaoMes" required placeholder="Mês" maxlength="2">
          <input type="text" v-model="dadosCliente.expiracaoAno" required placeholder="Ano" maxlength="4">
        </div>
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

    <!-- Exibindo mensagem de sucesso após compra -->
    <div v-if="compraProcessada.value" class="sucesso">
      <h2>Compra Finalizada com Sucesso!</h2>
    </div>
  </div>
</template>

<style scoped>
@import url("../assets/pagamento.css");
</style>
