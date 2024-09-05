<template>

<section class="container-login">
        <form class="container-login-form" name="form">
            <h1 class="container-login-titulo"> Cadastro</h1>
            <p> Você já tem uma conta? acesse o seu Login. <a href="./Login.html" target="_top"> Clique aqui</a></p>
            <div class="container-login-form-senha">
            <label class="container-login-label">
                <p class="contaier-login-texto">Nome Completo</p>
                <input type="text" required placeholder="Digie seu nome" class="container-login-input" name="user">
            </label>
            <label class="container-login-label">
                <p class="contaier-login-texto">Nome de Usuário</p>
                <input type="text" required placeholder="Digie seu usuário" class="container-login-input" name="user">
            </label>
        </div>
        <div class="container-login-form-senha">
            <label class="container-login-label">
                <p class="contaier-login-texto">Email</p>
                <input type="email" required placeholder="Digie seu Email" class="container-login-input" name="user">
            </label>
            <label class="container-login-label">
                <p class="contaier-login-texto">Data de Nascimento</p>
                <input type="date" required class="container-login-input" name="user">
            </label>
        </div>
            <div class="container-login-form-senha">
                <label class="container-login-label">
                    <p class="contaier-login-texto">Senha</p>
                <input type="password" required minlength="3" placeholder="Digite sua senha" class="container-login-input" name="password">
                </label>
                <label class="container-login-label">
                    <p class="contaier-login-texto">Confirme Sua senha</p>
                <input type="password" required minlength="3" placeholder="Confirme Sua senha" class="container-login-input" name="password">
                </label>
            </div>
            <h2 class="container-login-endereco">Endereço</h2>
            <label class="container-login-label">
                <input placeholder="Digite sua Rua" type="text" required  class="container-login-input"/>
                 <input placeholder="Digite seu Número" type="number" required class="container-login-input"/>
            </label>
        
            <label class="container-login-label">
                <input placeholder="Digite seu Bairro"type="text" required class="container-login-input"/> 
                <input placeholder="Digite seu CEP"type="number" required class="container-login-input"/>
            </label>
            <label class="container-login-label">
                <input placeholder="Digite sua Cidade"type="text" required class="container-login-input"/>
                <input placeholder="Digite seu Estado"type="text" required class="container-login-input"/>
            </label>
            <button class="container-login-botao">Cadastrar</button>
        </form>
    </section>
</template>