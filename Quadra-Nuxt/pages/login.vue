<style>

@import url('../assets/login.css');
</style>




0
<template>

<section class="container-login">
        <form class="container-login-form" name="form" onsubmit="verify(event)">
            <h1 class="container-login-titulo">Login</h1>
            <label class="container-login-label">
                <p class="contaier-login-texto">User</p>
                <input type="text" required placeholder="Digie seu usuário" class="container-login-input" name="user">
            </label>
            <label class="container-login-label">
                <p class="contaier-login-texto">Password</p>
            <input type="password" required minlength="3" placeholder="Digite sua senha" class="container-login-input" name="password">
            </label>
            <a href="esqueci.html" class="container-login-link">Esqueci minha Senha!</a>
            <button class="container-login-botao">Entrar</button>
            <p class="contaier-login-texto-cadastro">Não tem uma conta? <NuxtLink to="/cadastrar" class="container-login-link-cadastro">Cadastre!</NuxtLink></p>
        </form>
    </section>

</template>