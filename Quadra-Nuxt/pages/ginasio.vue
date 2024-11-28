<script setup>

    const params = defineProps(["alteraAlugado"])
    let data = ref("")
    let horas = ref("")

    function pagar(){
        console.log(data.value)
        localStorage.setItem("data", JSON.stringify( data.value));
        window.location.href = "/pagamento";
    }


    let quadraSelecionada = ref(null);

 
    onMounted(()=>{
        quadraSelecionada.value = JSON.parse( localStorage.getItem("quadraSelecionada") )
    })

</script>


<template>

    <section v-if="quadraSelecionada != null" >
        <h2 class="div1"> <strong>{{ quadraSelecionada.name }}</strong></h2>
        <div class="conteiner">

            <img v-bind:src="quadraSelecionada.photos" class="img"/>

            <div class="div2">
                <h3> {{ quadraSelecionada.name }} </h3>
                <!-- <p>Uma quadra para você jogar com amigos, com seu time em Campeonato!</p> -->
                <p> Preço </p>
                <p> R$ {{ quadraSelecionada.preco }}</p>

                <input type="date" class="cabecalho_menu_link_login" v-model="data"> - <input type="time" class="cabecalho_menu_link_login" v-model="horas">

                <br/>
                <br/>

                <a href="#" class="cabecalho_menu_link_login" v-on:click="pagar(quadraSelecionada.id)">Pagar</a>
            </div>

        </div>

        <br/>
        <br/>

        <p class="p3">
            O ginásio foi viabilizados através de um Decreto Municipal.
            Em 28 de novembro de 2010, o então prefeito Oswaldo Barba, 
            inaugurou os novos vestiários do ginásio que foram totalmente 
            remodelados, e a reforma da cobertura.
        </p>

    </section>



</template>

<style>

    @import url(../assets/ginasio.css);


</style>