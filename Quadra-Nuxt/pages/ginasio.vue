<script setup>

    const params = defineProps(["alteraAlugado","quadraSelecionada"])

    let data = ref("")
    let horas = ref("")

    function Alugar(){
        params.alteraAlugado(params.quadraSelecionada.id,data,horas)
        alert("Quadra Alugado com sucesso!")
        //window.location.href = "/perfil"
    }

</script>


<template>

    <section>
        <h2 class="div1"> <strong>Ginásio Redenção</strong></h2>
        <div class="conteiner">

            <img v-bind:src="params.quadraSelecionada.image" class="img"/>

            <div class="div2">
                <h3> <strong> {{ params.quadraSelecionada.nome }} </strong> </h3>
                <!-- <p>Uma quadra para você jogar com amigos, com seu time em Campeonato!</p> -->
                <p> <strong> Preço </strong> </p>
                <p> <strong>R$ </strong> {{ params.quadraSelecionada.preco }}</p>

                <input type="date" class="cabecalho_menu_link_login" v-model="data"> - <input type="time" class="cabecalho_menu_link_login" v-model="horas">

                <br/>
                <br/>

                <a href="#" class="cabecalho_menu_link_login" v-on:click="Alugar()">Alugar</a>
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