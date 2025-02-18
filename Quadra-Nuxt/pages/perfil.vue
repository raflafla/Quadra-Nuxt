<script setup>
import axios from 'axios';

const params = defineProps(["alteraAlugado","users"]);
console.log(params.quadras);

const location = reactive([]);
const quadras = reactive([]);


async function buscartodos(){
    let resposta = await axios.get('http://10.60.44.33:3001/location/read')
    location.value = resposta.data.db
    await Promise.all(location.value.map(l => buscaquadra(l.idcourt)));    
}

async function buscaquadra(id){
    let resposta = await axios.get(`http://10.60.44.33:3001/quadra/show/${id}`)
    quadras[id] = resposta.data.db
    
}

const user = ref(null);

function Sair() {
    localStorage.removeItem('user');
    window.location.href = "/";
}

onMounted(() => {
  const storedUser = localStorage.getItem('user');
  if (storedUser) {
    user.value = JSON.parse(storedUser);
  }
  buscartodos();
})
</script>

<template>
    <section class="cards-container">
        <a href="###" class="card">
            <div class="card-header">
                <img src="https://i.redd.it/t32e9rm0j1511.jpg" alt="Foto de Perfil do Cliente" class="perfil-imagem"/>
                <h2>Dados Pessoais:</h2>
            </div>

            <div class="card-content card-description">
                <div v-if="user">
                    <p>Nome: {{ user.name }}</p>
                    <p>Email: {{ user.email }}</p>
                    <p>Telefone: {{ user.phone }}</p>
                </div>
                <div v-else>
                    <p>Nenhum usuário autenticado.</p>
                </div>
            </div>

            <!-- Botão Sair dentro do card -->
            <div class="Sair" v-on:click="Sair()">
                <p class="fa-solid fa-door-open"> Sair</p>
            </div>
        </a>    
    </section>

    <section>
        <h1 class="titulo">Histórico de Quadras</h1>
   

    <div class="secao-p" v-for="l in location.value">
        <p>{{ l.date }}</p>
        <quadra v-bind:quadra="quadras[l.idcourt]" v-bind:telaorigem="'perfil'"/>
    </div>
</section>
</template>

<style>
@import url(../assets/perfil.css);
</style>
