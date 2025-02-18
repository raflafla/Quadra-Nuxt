<script setup>
    import axios from 'axios';

    const quadras = reactive([])

    async function buscartodos(){
        let resposta = await axios.get('http://10.60.44.33:3001/quadra/read')
        quadras.value = resposta.data.db
        console.log(quadras.value)
    }

    onMounted(() => {
        buscartodos()
        console.log('aqui')
    });
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto+Mono:ital,wght@0,100..700;1,100..700&display=swap');

:root{
    --cor-background: rgb(31, 31, 31);
    --cor-navbar: rgb(24, 24, 24);
    --cor-principal: #c34de4;
    --cor-secundaria: #9d2baf;
    --cor-texto: white;
    --cor-borda: #9d2baf;
    --cor-hover: #682a65;
}

body{
    margin: 0;
    background-color:  var(--cor-background);
    font-family: "Roboto Mono", monospace;
    color: var(--cor-texto);
}

strong{
    color: var(--cor-principal);
}

.resumo-principal{
    display: flex;
    margin: 50px 100px;
    justify-content: center;
    align-items: center;
    gap: 30px;
    flex-wrap: wrap;
    background-color: var(--cor-navbar);
    border-radius: 15px;
    padding: 30px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
}

.resumo-principal-texto{
    font-size: 1.1rem;
    display: flex;
    flex-direction: column;
    max-width: 580px;
    text-align: justify;
    color: var(--cor-texto);
}

.resumo-principal-imagem{
    max-width: 500px;
    border-radius: 15px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
}

.resumo-principal-botao{
    color: white;
    font-size: 1rem;
    text-decoration: none;
    padding: 10px 30px;
    border-radius: 30px;
    background-color: var(--cor-principal);
    align-self: center; 
    text-align: center;
    width: fit-content;
    transition: background-color 0.3s;
}

.resumo-principal-botao:hover{
    background-color: var(--cor-hover);
}

.resumo-principal-titulo{
    align-self: center;
    font-size: 2rem;
    font-weight: bold;
    margin-bottom: 20px;
}

.section-quem-somos{
    display: flex;
    margin: 50px;
    justify-content: center;
    gap: 30px;
    align-items: center;
}

.section-quem-somos-container{
    font-size: 1.1rem;
    max-width: 580px;
    text-align: justify;
    color: var(--cor-texto);
}

.section-quem-somos-imagem{
    width: 400px;
    height: 400px;
    border-radius: 15px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
}

.section-quem-somos-titulo{
    text-align: center;
    font-size: 1.8rem;
    margin-bottom: 20px;
    color: var(--cor-principal);
}

.secao{
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    gap: 20px;
}

.secao-titulo{
    text-align: center;
    font-size: 2rem;
    margin-top: 40px;
    color: var(--cor-principal);
}

.quadra-card{
    background: var(--cor-secundaria);
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    padding: 20px;
    max-width: 300px;
    width: 100%;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    text-align: center;
}

.quadra-card:hover{
    transform: translateY(-5px);
    box-shadow: 0 8px 15px rgba(0, 0, 0, 0.2);
}

.quadra-card h3{
    font-size: 1.5rem;
    color: var(--cor-texto);
    margin-bottom: 10px;
}

.quadra-card p{
    font-size: 1rem;
    color: var(--cor-texto);
}

.quadra-card .btn{
    display: inline-block;
    background-color: var(--cor-principal);
    color: var(--cor-texto);
    padding: 10px 20px;
    border-radius: 30px;
    text-decoration: none;
    margin-top: 10px;
    transition: background-color 0.3s;
}

.quadra-card .btn:hover{
    background-color: var(--cor-hover);
}

</style>

<template>
    <section class="resumo-principal">
        <img src="../public/imagem1.png" alt="" class="resumo-principal-imagem">
        <div class="resumo-principal-texto">
            <h1 class="resumo-principal-titulo">Seja Bem-vindo!</h1>
            <p>Você está procurando uma quadra de esportes para jogar com seus amigos, organizar um torneio ou simplesmente praticar seu esporte favorito? Nós estamos aqui para ajudar!</p>
            <p>Na <strong>Quadra Finder</strong>, facilitamos sua busca por quadras de esportes disponíveis para aluguel perto de você. Com apenas alguns cliques, você pode encontrar a quadra perfeita para futebol, basquete, vôlei, tênis e muito mais. Nossa plataforma é intuitiva e fácil de usar, permitindo que você veja a disponibilidade em tempo real, compare preços e faça reservas diretamente online.</p>
            <a href="quadras" class="resumo-principal-botao">Quadras</a>
        </div>
    </section>


    <section class="secao">
        <template v-for="quadra in quadras" :key="quadra.id">
            <div class="quadra-card">
                <h3>{{ quadra.nome }}</h3>
                <p>{{ quadra.descricao }}</p>
                <a :href="'/quadra/' + quadra.id" class="btn">Ver Detalhes</a>
            </div>
        </template>
    </section>

    <section class="section-quem-somos">
        <div class="section-quem-somos-container">
            <h2 class="section-quem-somos-titulo">Quem Somos?</h2>
            <p>Somos uma equipe apaixonada por esportes e tecnologia, com o objetivo de tornar a prática esportiva mais acessível para todos. Nosso foco é oferecer uma plataforma que simplifique a busca por quadras e facilite a reserva de espaços, tornando o processo mais eficiente e prático para usuários de todas as idades.</p>
            <p>No Quadra Finder, acreditamos que o esporte é uma ferramenta poderosa para melhorar a qualidade de vida, promover o bem-estar e unir pessoas. Por isso, trabalhamos para garantir que nossos usuários encontrem facilmente o local ideal para a prática esportiva, com informações claras sobre disponibilidade, preços e avaliações.</p>
        </div>
        <img src="../public/shshshshs.webp" alt="" class="section-quem-somos-imagem">
    </section>

</template>
