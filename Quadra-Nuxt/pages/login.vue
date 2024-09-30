<script setup>
    const params = defineProps(["users"])
    let email = ref("")
    let pass = ref("")
    
    
    let user = {
        name: "", pass: "", cpf: "", email: "", phone: "", type: "" ,
    }

    function authenticate(){
         params.users.map(u => {
            
            if(u.email == email.value && u.pass == pass.value){
                
                user = u
            }
        } )

        if(user.name == "" || user.name == null){
            alert("User não encontrado ")
            localStorage.removeItem("user")
            return
        }

        localStorage.setItem("user", JSON.stringify(user))
        alert("Autenticado com sucesso")
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