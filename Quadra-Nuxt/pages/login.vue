<script setup>
import axios from "axios";
import { ref, onMounted } from "vue";

const email = ref("");
const pass = ref("");
const users = ref([]);

async function buscartodos() {
    try {
        let resposta = await axios.get('http://10.60.44.32:3000/user/read');
        users.value = resposta.data.list_users;
        console.log(users.value);
    } catch (error) {
        console.error("Erro ao buscar usuários:", error);
    }
}

onMounted(() => {
    buscartodos();
});

function authenticate() {
    const user = users.value.find(u => u.email === email.value && u.pass === pass.value);

    if (!user) {
        alert("Usuário não encontrado");
        localStorage.removeItem("user");
        return;
    }

    localStorage.setItem("user", JSON.stringify(user));
    alert("Autenticado com sucesso");
    window.location.href = '/';
}
</script>







<style scoped>

@import url('../assets/login.css');
</style>

0
<template>

<section class="container-login">
        <form class="container-login-form" name="form" v-on:submit.prevent="authenticate()">
            <h1 class="container-login-titulo">Login</h1>
            <label class="container-login-label">
                <p class="contaier-login-texto">Email</p>
                <input type="text" required placeholder="Digie seu usuário" class="container-login-input" name="user" v-model="email">
            </label>
            <label class="container-login-label">
                <p class="contaier-login-texto">Password</p>
            <input type="password" required minlength="3" placeholder="Digite sua senha" class="container-login-input" name="password" v-model="pass">
            </label>
            <a href="esqueci.html" class="container-login-link">Esqueci minha Senha!</a>
            <button class="container-login-botao">Entrar</button>
            <p class="contaier-login-texto-cadastro">Não tem uma conta? <NuxtLink to="/cadastrar" class="container-login-link-cadastro">Cadastre!</NuxtLink></p>
        </form>
    </section>

</template>