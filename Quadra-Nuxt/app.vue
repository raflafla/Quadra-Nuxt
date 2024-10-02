<script setup> 

const quadras = reactive([
        {
            id: 0,
            nome: "Campo Society 1",
            preco: 22.90,
            alugado: true,
            image: ""
        },
        {
            id: 1,
            nome: "Campo Society 2",
            preco: 12.90,
            alugado: true,
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



    const users = reactive([
    { name: "João", pass: "123", cpf: "123.456.789-00", email: "joao@example.com", phone: "(11) 91234-5678", type: "padrão" },
    { name: "Maria", pass: "123", cpf: "987.654.321-00", email: "maria@example.com", phone: "(21) 98765-4321", type: "padrão" },
    { name: "Carlos", pass: "123", cpf: "111.222.333-44", email: "carlos@example.com", phone: "(31) 99876-5432", type: "padrão" },
    { name: "Ana", pass: "123", cpf: "555.666.777-88", email: "ana@example.com", phone: "(41) 99888-9999", type: "padrão" },
    { name: "Luiz", pass: "123", cpf: "222.333.444-55", email: "luiz@example.com", phone: "(51) 98765-1234", type: "padrão" },
    ])


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
  <NuxtPage v-bind:quadras="quadras" v-bind:alteraAlugado="alteraAlugado" v-bind:users="users"/>
  <Footerb />

</template>
