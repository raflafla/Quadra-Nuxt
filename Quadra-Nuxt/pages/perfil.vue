
[<style scoped>

@import url('../assets/perfil.css');
</style>

<script setup>


const params = defineProps(["quadras", "alteraAlugado","users"])


import { ref, onMounted } from 'vue'


const user = ref(null)


function Sair(){
    localStorage.removeItem('user')
    window.location.href = "/"
}

onMounted(() => {
  const storedUser = localStorage.getItem('user')
  if (storedUser) {
    user.value = JSON.parse(storedUser)
  }
})



</script>


<template>

<section class="cards-container">
    <a href="###" class="card">

    <div class="card-header">

        <img src="https://i.redd.it/t32e9rm0j1511.jpg" alt="Foto de Perfil do Cliente" class="perfil-imagem"/>

        <h2>Dados Pessoais:</h2>
    </div>

     <div class="card-content card-description" >
    
    <div v-if="user">

        <p>Nome:{{ user.name }}</p>

        <p>Email:{{ user.email }}</p>

        <p>Telefone:{{ user.phone }}</p>

    </div>

    <div v-else>

        <p>Nenhum usuário autenticado.</p>

    </div>

    
    </div>
    <div class="Sair" v-on:click="Sair()">
         <p class="fa-solid fa-door-open " style="color: white;"> Sair</p> 
    </div>

    </a>    
    </section>

    <section>

        <div class="titulo">
        <h1>Histórico de Quadras</h1>

            <div v-for="quadra in quadras">
                <quadra v-if=" quadra.alugado == true" v-bind:quadras="quadra" v-bind:alteraAlugado="alteraAlugado"/>
            </div>

    </div>

    </section>

   

</template>