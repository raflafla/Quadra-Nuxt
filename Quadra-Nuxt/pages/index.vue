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
            <a href="#" class="resumo-principal-botao">Quadras</a>
        </div>
    </section>

        <h1 class="secao-titulo">Quadras Populares</h1>
        <section class="secao">
            <quadra v-bind:quadras="quadras", v-for="quadra in quadras"/>
        </section>


    <section class="section-quem-somos">
        <div class="section-quem-somos-container">
            <h2 class="section-quem-somos-titulo">Quem Somos?</h2>
            <p class="section-quem-somos-texto">
            Lorem ipsum dolor, sit amet consectetur adipisicing elit. Cum fuga consequuntur esse quibusdam reprehenderit ipsa amet magnam enim. Ad veritati
            s laborum quis expedita nihil est rem architecto tempore accusantium recusandae. </p>
            <p class="section-quem-somos-texto">
                Lorem ipsum dolor, sit amet consectetur adipisicing elit. Cum fuga consequuntur esse quibusdam reprehenderit ipsa amet magnam enim. Ad veritati
                s laborum quis expedita nihil est rem architecto tempore accusantium recusandae. </p>
            <p class="section-quem-somos-texto">
                Lorem ipsum dolor, sit amet consectetur adipisicing elit. Cum fuga consequuntur esse quibusdam reprehenderit ipsa amet magnam enim. Ad veritati
                s laborum quis expedita nihil est rem architecto tempore accusantium recusandae. </p>
        </div>
        <img src="../public/shshshshs.jpg" alt="" class="section-quem-somos-imagem">
    </section>

</template>