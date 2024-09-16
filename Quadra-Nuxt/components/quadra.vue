<script setup>

const params = defineProps(["quadras", "alteraAlugado"])


</script>



<style scoped>
@import url(../assets/quadras.css);
</style>


<template>

        <div class="secao-item">
            <h2 class="secao-item-titulo">{{ params.quadras.nome }}</h2>
            <p class="secao-item-texto"></p>
            <img src="" alt="Cruiser" width="300px" class="secao-item-imagem">
            <p class="secao-item-valor">{{ params.quadras.preco }}</p>
            <a  href="#" class="secao-item-botao">Alugar</a>
        </div>
        
</template>