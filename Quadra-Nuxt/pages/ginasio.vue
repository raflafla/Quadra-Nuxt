<script setup>
    const params = defineProps(["alteraAlugado"])
    let data = ref("")
    let horas = ref("")

    function pagar(){
        console.log(data.value)
        localStorage.setItem("data", JSON.stringify(data.value));
        window.location.href = "/pagamento";
    }

    let quadraSelecionada = ref(null);

    onMounted(() => {
        quadraSelecionada.value = JSON.parse(localStorage.getItem("quadraSelecionada"))
    })
</script>

<template>
    <section v-if="quadraSelecionada != null">
        <h2 class="titulo-quadra"> <strong>{{ quadraSelecionada.name }}</strong></h2>
        
        <div class="container">
            <img v-bind:src="quadraSelecionada.photos" class="imagem-quadra"/>

            <div class="info-quadra">
                <h3> {{ quadraSelecionada.name }} </h3>
                <p class="preco">Preço</p>
                <p class="preco-valor"> {{ quadraSelecionada.preco }}</p>

                <div class="inputs-data">
                    <input type="date" class="input-data" v-model="data">
                    <input type="time" class="input-hora" v-model="horas">
                </div>

                <br/>

                <a href="#" class="botao-pagar" v-on:click="pagar(quadraSelecionada.id)">Pagar</a>
            </div>
        </div>

        <br/>
        <br/>

        <p class="descricao-quadra">
            O ginásio foi viabilizado através de um Decreto Municipal. Em 28 de novembro de 2010, o então prefeito Oswaldo Barba, 
            inaugurou os novos vestiários do ginásio, que foram totalmente remodelados, e a reforma da cobertura.
        </p>
    </section>
</template>

<style>
@import url(../assets/ginasio.css);
</style>
    