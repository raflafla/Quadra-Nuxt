<script setup>
import axios from 'axios';

const quadras = reactive([])

async function buscartodos(){
    let resposta = await axios.get('http://localhost:3000/quadra/read')
    console.log(resposta)
}



onMounted(() => {
    buscartodos()
    console.log('aqui')
});


</script>


<template>


    <h1 class="titulo-quadras">Catálogo Quadras</h1>
    <section class="secao">

        <template v-for="quadra in quadras"> 
            
            <quadra v-if="quadra.alugado == false" v-bind:quadras="quadra" />
        </template>

        
    </section>
</template>

<style scoped>
@import url(../assets/quadras.css);
</style>