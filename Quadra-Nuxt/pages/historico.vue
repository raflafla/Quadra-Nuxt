<style scoped>
  @import url('../assets/historico.css');
</style>

<script setup>

const params = defineProps(["quadras", "alteraAlugado"])

</script>



<template>

    <div>


      <h1 class="secao-titulo">Histórico de Quadras</h1>

      <div v-for="quadra in quadras">
        <quadra v-if=" quadra.alugado == true" v-bind:quadras="quadra" v-bind:alteraAlugado="alteraAlugado"/>
        
      </div>
  
      

    </div>


</template>
  
  
  
  
  