
[<style scoped>

@import url('../assets/perfil.css');
</style>

<script setup>

const params = defineProps(["quadras", "alteraAlugado"])

</script>


<template>

<section class="cards-container">
    <a href="###" class="card">

    <div class="card-header">

        <img src="https://i.redd.it/t32e9rm0j1511.jpg" alt="Foto de Perfil do Cliente" class="perfil-imagem"/>

    </div>

     <div class="card-content card-description" >

        <h2>Nome: </h2>
        <p>email:</p>


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