<script setup>


     const params = defineProps (["quadras", "alteraAlugado"]); 



</script>



<template>

<div class="conteudo">
    <p>{{ params.quadras.nome }}</p>
 
    <p v-if="params.quadras.alugado == true"> <u>Alugado</u> </p>

    <img src="..//public/grama.jpg"/>

    <p> R$ {{ params.quadras. }}</p>

    <button v-on:click="params.alteraAlugado(params.quadras.id)" v-if="params.quadras.alugado == false" class="button">Alugar</button>
</div>


</template>

<style scoped>
    
    

</style>