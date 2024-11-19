<script setup> 


    function alteraAlugado(id,data,horas){
        quadras.map((q)=>{
            if(q.id == id){
                q.alugado = true
                q.data = data
                q.horas = horas
            }
        })
    }



    const isLoggedIn = ref(false);

    onMounted(() => {
    if (typeof window !== 'undefined') {
        isLoggedIn.value = localStorage.getItem('user') !== null;
    }
});

</script>




<style>
@import url("./assets/index.css");
</style>



<template>
  <Head>
    <Script src="https://kit.fontawesome.com/e9b73e9254.js" crossorigin="anonymous"></Script>
  </Head>


    <nava v-if="isLoggedIn"/>
    <navb  v-if="isLoggedIn == false"/>
  <NuxtPage v-bind:quadras="quadras" v-bind:alteraAlugado="alteraAlugado" v-bind:users="users" v-bind:quadraSelecionada="quadraSelecionada" v-bind:atualizaQuadraSelecionada="atualizaQuadraSelecionada"/>
  <Footerb />

</template>
