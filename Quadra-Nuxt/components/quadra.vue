<script setup>


const params = defineProps(["quadra", "quadraSelecionada"])

 function alugar(){
    localStorage.setItem("quadraSelecionada", JSON.stringify( params.quadra));
    window.location.href = "/ginasio";
}

</script>


<template>

        <div class="secao-item" v-if="quadra">
            <h2 class="secao-item-titulo">{{ params.quadra.name }}</h2>
            <p class="secao-item-texto"></p>
            <img v-bind:src="params.quadra.photos" alt="" width="300px" class="secao-item-imagem">
            <p class="secao-item-valor">{{ params.quadra.preco }}</p>
            <a href="#" class="secao-item-botao" v-on:click="alugar()"> {{params.quadra.alugado}} </a>
        </div>
        
</template>



<style scoped>
@import url("../assets/quadras.css");
</style>