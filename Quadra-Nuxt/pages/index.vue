<script setup>
    const params = defineProps(["quadras", "alteraAlugado"])
    // vue emit
</script>

<style scoped>
@import url(../assets/index.css);

</style>



<template>
        <section class="resumo-principal">
        <img src="../public/imagem1.png" alt="" class="resumo-principal-imagem">
        <div class="resumo-principal-texto">
            <h1 class="resumo-principal-titulo">Seja Bem vindo!</h1>
            <p>Você está procurando uma quadra de esportes para jogar com seus amigos, organizar um torneio ou simplesmente praticar seu esporte favorito? Nós estamos aqui para ajudar!</p>
            <p> Na <strong>Quadra Finder</strong>, facilitamos sua busca por quadras de esportes disponíveis para aluguel perto de você. Com apenas alguns cliques, 
            você pode encontrar a quadra perfeita para futebol, basquete, vôlei, tênis e muito mais. Nossa plataforma é intuitiva e fácil de usar, permitindo que você veja a 
            disponibilidade em tempo real, compare preços e faça reservas diretamente online.</p>
            <a href="quadras" class="resumo-principal-botao">Quadras</a>
        </div>
    </section>

        <h1 class="secao-titulo">Quadras Populares</h1>
        <section class="secao">
            <div class="secao-item">
            <h2 class="secao-item-titulo">Quadra</h2>
            <p class="secao-item-texto"></p>
            <img alt="" width="300px" class="secao-item-imagem">
            <p class="secao-item-valor">R$ 20</p>
            <a href="#" class="secao-item-botao" v-on:click="alugar()"> Alugar </a>
        </div>
        <div class="secao-item">
            <h2 class="secao-item-titulo">Quadra</h2>
            <p class="secao-item-texto"></p>
            <img alt="" width="300px" class="secao-item-imagem">
            <p class="secao-item-valor">R$ 20</p>
            <a href="#" class="secao-item-botao" v-on:click="alugar()"> Alugar </a>
        </div>
        <div class="secao-item">
            <h2 class="secao-item-titulo">Quadra</h2>
            <p class="secao-item-texto"></p>
            <img src="" alt="" width="300px" class="secao-item-imagem">
            <p class="secao-item-valor">R$ 20</p>
            <a href="#" class="secao-item-botao" v-on:click="alugar()"> Alugar </a>
        </div>
        </section>


    <section class="section-quem-somos">
        <div class="section-quem-somos-container">
            <h2 class="section-quem-somos-titulo">Quem Somos?</h2>
            <p class="section-quem-somos-texto">
                Somos uma equipe apaixonada por esportes e tecnologia, com o objetivo de tornar a prática esportiva mais acessível para todos. Nosso foco é oferecer uma plataforma que simplifique a busca por quadras e facilite a reserva de espaços, tornando o processo mais eficiente e prático para usuários de todas as idades. </p>
            <p class="section-quem-somos-texto">
                No Quadra Finder, acreditamos que o esporte é uma ferramenta poderosa para melhorar a qualidade de vida, promover o bem-estar e unir pessoas. Por isso, trabalhamos para garantir que nossos usuários encontrem facilmente o local ideal para a prática esportiva, com informações claras sobre disponibilidade, preços e avaliações.

 </p>
        </div>
        <img src="../public/shshshshs.webp" alt="" class="section-quem-somos-imagem">
    </section>

</template>