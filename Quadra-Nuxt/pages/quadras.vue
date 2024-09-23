<script setup>


const params = defineProps(["quadras"])
</script>



<style scoped>
@import url(../assets/quadras.css);
</style>

<template>
    <h1 class="titulo-quadras">Catálogo Quadras</h1>
    <section class="secao">

        <quadra v-bind:quadras="quadras" v-for="quadra in quadras"/>

        
    </section>
</template>