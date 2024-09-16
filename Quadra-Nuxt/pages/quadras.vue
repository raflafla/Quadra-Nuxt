<script setup>


const params = defineProps(["quadras"])
</script>



<style scoped>
@import url(../assets/quadras.css);
</style>

<template>
    <h1 class="titulo-quadras">Catálogo Quadras</h1>
    <section class="secao">
        <quadra v-bind:quadras="quadras[0]"/>
        <quadra v-bind:quadras="quadras[1]"/>   
        <quadra v-bind:quadras="quadras[2]"/>

        <quadra v-bind:quadras="quadras[0]"/>
        <quadra v-bind:quadras="quadras[1]"/>
        <quadra v-bind:quadras="quadras[2]"/>
    
        
    </section>
</template>