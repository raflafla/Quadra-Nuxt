<script setup> 

const quadras = reactive([
        {
            id: 0,
            nome: "Campo Society 1",
            preco: 22.90,
            alugado: false,
            image: ""
        },
        {
            id: 1,
            nome: "Campo Society 2",
            preco: 12.90,
            alugado: false,
            image: ""
        },
        {
            id: 2,
            nome: "Campo Society 3",
            preco: 25.90,
            alugado: false,
            image: ""
        }
    ])

    function alteraAlugado(id){
    quadras[id].alugado = true;
}


</script>




<style>
@import url("./assets/index.css");
</style>



<template>
  <Head>
    <Script src="https://kit.fontawesome.com/e9b73e9254.js" crossorigin="anonymous"></Script>
  </Head>



  <navb  />
  <NuxtPage v-bind:quadras="quadras" v-bind:alteraAlugado="alteraAlugado"/>
  <Footerb />

</template>
