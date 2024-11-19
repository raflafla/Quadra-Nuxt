
<script setup>
import axios from 'axios';

const user = reactive([])

async function buscartodos(){
    let resposta = await axios.get('http://10.60.44.36:3000/user/read')
    user.value = resposta
    console.log(user.value)
}


async function sendform (){

    if(user.pass != confirm.value){
        alert("Senha não compativeis")
        return
    }
    await axios.post('http://10.60.44.36:3000/user/create', {
        name: user.name, 
        pass: user.pass,
        cpf: user.cpf,
        email: user.email,
        phone: user.phone

    })
    alert("Cadastro feito com sucesso")
    console.log(params.users)
    window.location.href='/'
}

onMounted(() => {
    buscartodos()
    console.log('aqui')
});

function VerificaLogado(){
    if( localStorage.getItem("user") ){
      //localStorage.removeItem("user")
      window.location.href='/'
    }
}




onMounted(() => {
    VerificaLogado();
})
</script>



<style scoped>
@import url('../assets/Cadastro.css');
</style>



<template>

<section class="container-login">
        <form class="container-login-form" name="form" v-on:submit.prevent="sendform()">
            <h1 class="container-login-titulo"> Cadastro</h1>
            <p> Você já tem uma conta? acesse o seu Login. <NuxtLink to="/login"> Clique aqui</NuxtLink></p>
            <div class="container-login-form-senha">
            <label class="container-login-label">
                <p class="contaier-login-texto">Nome Completo</p>
                <input type="text" required placeholder="Digie seu nome" class="container-login-input" name="user" v-model="user.name">
            </label>
        </div>
        <div class="container-login-form-senha">
            <label class="container-login-label">
                <p class="contaier-login-texto">Email</p>
                <input type="email" required placeholder="Digie seu Email" class="container-login-input" name="user" v-model="user.email">
            </label>

            <label class="container-login-label">
                <p class="contaier-login-texto">CPF</p>
                <input type="" required placeholder="Digie seu CPF" class="container-login-input" name="user" v-model="user.cpf">
            </label>
        </div>
        <div class="container-login-form-senha">
            <label class="container-login-label">
                <p class="contaier-login-texto">Phone</p>
                <input type="" required placeholder="Digie seu Phone" class="container-login-input" name="user" v-model="user.phone">
            </label>
        </div>
            <div class="container-login-form-senha">
                <label class="container-login-label">
                    <p class="contaier-login-texto">Senha</p>
                <input type="password" required minlength="3" placeholder="Digite sua senha" class="container-login-input" name="password" v-model="user.pass">
                </label>
                <label class="container-login-label">
                    <p class="contaier-login-texto">Confirme Sua senha</p>
                <input type="password" required minlength="3" placeholder="Confirme Sua senha" class="container-login-input" name="password" v-model="confirm">
                </label>
            </div>
            <button class="container-login-botao">Cadastrar</button>
        </form>
    </section>
</template>