<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";


const user = ref({
    name: "",
    pass: "",
    confirmPass: "",
    cpf: "",
    email: "",
    phone: ""
});

const mensagem = ref("");
const tipoMensagem = ref(""); // "success" ou "error"
const showMensagem = ref(false);

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

async function sendform() {
    if (user.value.pass !== user.value.confirmPass) {
        showMessage("As senhas não coincidem!", "error");
        return;
    }

    if (!isEmailValid(user.value.email)) {
        showMessage("Por favor, insira um e-mail válido!", "error");
        return;
    }

    try {
        const response = await axios.post("http://10.60.44.33:3001/user/create", {
            name: user.value.name,
            pass: user.value.pass,
            cpf: user.value.cpf,
            email: user.value.email,
            phone: user.value.phone
        });

        if (response.status === 201 || response.status === 200) {
            showMessage("Cadastro feito com sucesso!", "success");
            setTimeout(() => {
                window.location.href = "/";
            }, 2000);
        } else {
            showMessage("Erro inesperado ao cadastrar.", "error");
        }
    } catch (error) {
        console.error("Erro ao cadastrar usuário:", error);
        showMessage("Erro ao realizar o cadastro.", "error");
    }
}

function VerificaLogado() {
    if (localStorage.getItem("user")) {
        window.location.href = "/";
    }
}

onMounted(() => {
    VerificaLogado();
});
</script>

<style scoped>
@import url("../assets/Cadastro.css");
</style>

<template>
    <section class="container-login">
        <form class="container-login-form" name="form" v-on:submit.prevent="sendform()">
            <h1 class="container-login-titulo">Cadastro</h1>
            <p>Você já tem uma conta? Acesse o seu Login. <NuxtLink to="/login">Clique aqui</NuxtLink></p>

            <div class="container-login-form-senha">
                <label class="container-login-label">
                    <p class="contaier-login-texto">Nome Completo</p>
                    <input type="text" required placeholder="Digite seu nome" class="container-login-input" v-model="user.name">
                </label>
            </div>

            <div class="container-login-form-senha">
                <label class="container-login-label">
                    <p class="contaier-login-texto">Email</p>
                    <input type="email" required placeholder="Digite seu Email" class="container-login-input" v-model="user.email">
                </label>

                <label class="container-login-label">
                    <p class="contaier-login-texto">CPF</p>
                    <input type="text" required placeholder="Digite seu CPF" class="container-login-input" v-model="user.cpf">
                </label>
            </div>

            <div class="container-login-form-senha">
                <label class="container-login-label">
                    <p class="contaier-login-texto">Telefone</p>
                    <input type="text" required placeholder="Digite seu Telefone" class="container-login-input" v-model="user.phone">
                </label>
            </div>

            <div class="container-login-form-senha">
                <label class="container-login-label">
                    <p class="contaier-login-texto">Senha</p>
                    <input type="password" required minlength="3" placeholder="Digite sua senha" class="container-login-input" v-model="user.pass">
                </label>
                <label class="container-login-label">
                    <p class="contaier-login-texto">Confirme sua senha</p>
                    <input type="password" required minlength="3" placeholder="Confirme sua senha" class="container-login-input" v-model="user.confirmPass">
                </label>
            </div>

            <button class="container-login-botao">Cadastrar</button>
        </form>

        <!-- Mensagem de erro ou sucesso -->
        <transition name="fade">
            <div v-if="showMensagem" :class="['message-box', tipoMensagem]">
                <span class="message-icon">
                    {{ tipoMensagem === 'success' ? '✅' : '❌' }}
                </span>
                {{ mensagem }}
            </div>
        </transition>
    </section>
</template>
