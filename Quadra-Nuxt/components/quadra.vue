<script setup>


const params = defineProps(["quadras", "quadraSelecionada"])

 function alugar(){
    localStorage.setItem("quadraSelecionada", JSON.stringify( params.quadras));
    window.location.href = "/ginasio";
}

</script>


<template>

        <div class="secao-item" v-if="quadras">
            <h2 class="secao-item-titulo">{{ params.quadras.nome }}</h2>
            <p class="secao-item-texto"></p>
            <img v-bind:src="params.quadras.image" alt="" width="300px" class="secao-item-imagem">
            <p class="secao-item-valor">{{ params.quadras.preco }}</p>
            <a href="#" class="secao-item-botao" v-on:click="alugar()"> Alugar </a>
        </div>
        
</template>



<style scoped>
@import url("../assets/quadras.css");
</style>