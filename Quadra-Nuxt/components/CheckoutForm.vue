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
    <div v-if="compraProcessada" class="sucesso">
      <h2>Compra Finalizada com Sucesso!</h2>
    </div>

    <!-- Exibindo mensagem de erro ao processar o pagamento -->
    <div v-if="erroPagamento" class="erro">
      <h2>{{ erroPagamento }}</h2>
    </div>
  </div>
</template>

<script setup>
  import axios from 'axios';

  // Inicializando como null para evitar acessar undefined
  const quadraSelecionada = ref(null);
  const userselecionado = ref(null)
  const data = ref(null);
  const horas = ref(null);

  // Mensagens de erro e sucesso
  const erroPagamento = ref(null); // Para erro no pagamento
  const sucessoCompra = ref(null); // Para mensagem de sucesso na compra

  // onMounted: Carregar quadra e data do localStorage
  onMounted(() => {
    const quadra = localStorage.getItem("quadraSelecionada");
    const user = localStorage.getItem("user");
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
    expiracaoMes: '',
    expiracaoAno: '',
    cvv: '',
    total: 0
  });

  const compraProcessada = ref(false);

  const processarCompra = async () => {
    erroPagamento.value = null; // Resetando o erro de pagamento

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
          erroPagamento.value = 'Quadra não selecionada. Por favor, tente novamente.';
          return;
        }

        // Criar a reserva de quadra
        let resposta = await axios.post('http://10.60.44.33:3001/location/create', {
          iduser: userselecionado.value.id,
          idcourt: quadraSelecionada.value.id,
          date: data.value
        });

        // Atualizar a quadra como 'alugada'
        await axios.put(`http://10.60.44.33:3001/quadra/update/${quadraSelecionada.value.id}`, {
          alugado: "Alugado"
        });

        const date = new Date();
        const formattedDate = date.toISOString().split('T')[0];

        let preco = quadraSelecionada.value.preco; // Exemplo: "R$ 100,50"
        let precoDecimal = parseFloat(preco.replace("R$", "").replace(",", ".").trim());

        await axios.post('http://10.60.44.33:3001/payment/create', {
          total: precoDecimal,
          date: formattedDate,
          iduser: userselecionado.value.id,
          idlocation: resposta.data.db.id,
          cvv: dadosCliente.cvv,
          numbercard: dadosCliente.cartao,
          yearcard: dadosCliente.expiracaoMes,
          monthcard: dadosCliente.expiracaoAno
        });

        compraProcessada.value = true;
        sucessoCompra.value = 'Compra realizada com sucesso!';
        window.location.href = "/perfil";

      } catch (error) {
        console.error('Erro ao processar a compra:', error);
        erroPagamento.value = 'Ocorreu um erro ao processar o pagamento. Tente novamente mais tarde.'; // Mensagem de erro
      }
    } else {
      erroPagamento.value = 'Por favor, preencha todos os campos corretamente.';
    }
  };
</script>

<style scoped>
@import url("../assets/pagamento.css");

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

.campo-expiracao {
  display: flex;
  gap: 10px; /* Espaçamento entre os campos */
}

.campo-expiracao input {
  width: 48%; /* Largura de cada campo, deixando espaço para os dois */
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

.erro {
  margin-top: 20px;
  background-color: #f8d7da;
  padding: 10px;
  border: 1px solid #f5c6cb;
  border-radius: 4px;
  color: #721c24;
  text-align: center;
} 
</style>
