<script setup>

const params = defineProps(["quadras"])


</script>


<template>


    <h1 class="titulo-quadras">Catálogo Quadras</h1>
    <section class="secao">

        <template v-for="quadra in params.quadras"> 
            
            <quadra v-if="quadra.alugado == false" v-bind:quadras="quadra" />
        </template>

        
    </section>
</template>

<style scoped>
@import url(../assets/quadras.css);
</style>