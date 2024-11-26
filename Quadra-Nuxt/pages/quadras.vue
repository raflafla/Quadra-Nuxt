<script setup>
import axios from 'axios';

const quadras = reactive([])

async function buscartodos(){
    let resposta = await axios.get('http://10.60.44.32:3000/quadra/read')
    quadras.value = resposta.data.db
    console.log(quadras.value)
    
}

function oi(){
    console.log(quadras.value[6].name)
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
            <quadra v-bind:quadra="quadra"/>
        </template>

        
    </section>
</template>

<style scoped>
@import url(../assets/quadras.css);
</style>