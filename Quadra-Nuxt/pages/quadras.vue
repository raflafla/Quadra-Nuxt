<script setup>


const params = defineProps(["quadras"])
</script>



<style scoped>
@import url(../assets/quadras.css);
</style>

<template>


    <h1 class="titulo-quadras">Catálogo Quadras</h1>
    <section class="secao">

        <div v-for="quadra in quadras"> 
            
            <quadra v-bind:quadras="quadra" />
        </div>

        
    </section>
</template>