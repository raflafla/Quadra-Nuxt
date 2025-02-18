<script setup>
import axios from "axios";
import { ref, onMounted } from "vue";

const email = ref("");
const pass = ref("");
const users = ref([]);
const mensagem = ref("");
const tipoMensagem = ref(""); // "success" ou "error"
const showMensagem = ref(false);

async function buscartodos() {
    try {
        let resposta = await axios.get('http://10.60.44.33:3001/user/read');
        users.value = resposta.data.list_users;
    } catch (error) {
        showMessage("Erro ao buscar usuários.", "error");
        console.error("Erro ao buscar usuários:", error);
    }
}

onMounted(() => {
    buscartodos();
});

// Função para exibir mensagens com transição
function showMessage(texto, tipo) {
    mensagem.value = texto;
    tipoMensagem.value = tipo;
    showMensagem.value = true;

    setTimeout(() => {
        showMensagem.value = false;
    }, 3000);
}

// Validação de e-mail
function isEmailValid(email) {
    const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return regex.test(email);
}

function authenticate() {
    if (!isEmailValid(email.value)) {
        showMessage("Por favor, insira um e-mail válido!", "error");
        return;
    }

    const user = users.value.find(u => u.email === email.value && u.pass === pass.value);

    if (!user) {
        showMessage("Usuário ou senha incorretos.", "error");
        localStorage.removeItem("user");
        return;
    }

    localStorage.setItem("user", JSON.stringify(user));
    showMessage("Login realizado com sucesso!", "success");

    setTimeout(() => {
        window.location.href = "/";
    }, 2000);
}

// Função para exibir mensagem ao clicar em "Esqueci minha senha"
function forgotPassword() {
    showMessage("Essa função está em desenvolvimento!", "error");
}
</script>

<style scoped>
@import url('../assets/login.css');
</style>

<template>
<section class="container-login">
    <form class="container-login-form" name="form" v-on:submit.prevent="authenticate()">
        <h1 class="container-login-titulo">Login</h1>
        <label class="container-login-label">
            <p class="contaier-login-texto">Email</p>
            <input type="text" required placeholder="Digite seu email" class="container-login-input" v-model="email">
        </label>
        <label class="container-login-label">
            <p class="contaier-login-texto">Senha</p>
            <input type="password" required minlength="3" placeholder="Digite sua senha" class="container-login-input" v-model="pass">
        </label>
        <a href="#" class="container-login-link" @click.prevent="forgotPassword">Esqueci minha Senha!</a>
        <button class="container-login-botao">Entrar</button>
        <p class="contaier-login-texto-cadastro">
            Não tem uma conta? 
            <NuxtLink to="/cadastrar" class="container-login-link-cadastro">Cadastre!</NuxtLink>
        </p>
    </form>

    <!-- Mensagem de erro/sucesso -->
    <div v-if="showMensagem" :class="['mensagem', tipoMensagem, 'show']">
        {{ mensagem }}
    </div>
</section>
</template>
