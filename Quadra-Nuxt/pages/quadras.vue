<script setup>
import axios from 'axios';

const quadras = reactive([])

async function buscartodos(){
    let resposta = await axios.get('http://10.60.44.36:3000/quadra/read')
    quadras.value = resposta.data.db
    console.log(quadras.value)
}



onMounted(() => {
    buscartodos()
    console.log('aqui')
});


</script>


<template>


    <h1 class="titulo-quadras">Catálogo Quadras</h1>
    <section class="secao">

        <template v-for="quadra in quadras.value"> 
            <quadra v-if="quadra.alugado == false" v-bind:quadra="quadra" />
        </template>

        
    </section>
</template>

<style scoped>
@import url(../assets/quadras.css);
</style>