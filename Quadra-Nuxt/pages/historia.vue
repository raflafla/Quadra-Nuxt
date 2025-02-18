<template>
    <section class="historia-container">
        <div class="historia-container-a">
            <h1 class="historia-titulo">Quem somos?</h1>
            <p class="historia-texto">
                Bem-vindo ao <strong>Quadra Finder</strong>, a plataforma inovadora que visa revolucionar a maneira como você encontra e reserva espaços para esportes. 
                Somos uma equipe apaixonada por promover a saúde e o bem-estar por meio da prática esportiva, e acreditamos que o acesso fácil a quadras de qualidade 
                deve ser uma realidade para todos. Aqui, o objetivo é garantir uma experiência intuitiva, rápida e acessível para todos os esportistas e entusiastas 
                de atividades físicas.
            </p>

            <div class="historia-funcionalidades">
                <h2 class="historia-subtitulo">Funcionalidades principais</h2>
                <ul class="historia-lista">
                    <li><strong>Busca personalizada:</strong> Encontre quadras perto de você de forma rápida e fácil, filtrando por localização, preço e tipo de esporte.</li>
                    <li><strong>Agendamento simples:</strong> Reserve a quadra desejada com apenas alguns cliques, e escolha o horário que melhor se encaixa na sua agenda.</li>
                    <li><strong>Pagamento seguro:</strong> Realize o pagamento online com total segurança e comodidade através de diversos métodos de pagamento.</li>
                    <li><strong>Notificações:</strong> Receba lembretes e atualizações em tempo real sobre sua reserva, garantindo que você nunca perca a hora.</li>
                    <li><strong>Histórico de reservas:</strong> Acompanhe todas as suas reservas passadas e futuras, garantindo que você tenha sempre um controle completo.</li>
                </ul>
            </div>

            <p class="historia-texto">
                Acreditamos que a prática de atividades físicas não deve ser limitada pelo acesso a espaços de qualidade, e é por isso que trabalhamos constantemente para 
                melhorar a nossa plataforma e oferecer a você a melhor experiência possível. 
                Nosso compromisso é com a saúde, a acessibilidade e, principalmente, com a sua experiência esportiva. 
                Com o <strong>Quadra Finder</strong>, reservar uma quadra nunca foi tão fácil.
            </p>

            <h2 class="historia-subtitulo">Nossos Benefícios</h2>
            <p class="historia-texto">
                Além das funcionalidades incríveis que você já conheceu, ao utilizar o <strong>Quadra Finder</strong>, você também conta com:
            </p>
            <ul class="historia-lista-beneficios">
                <li><strong>Quadras de alto padrão:</strong> Trabalhamos apenas com parceiros de confiança para garantir a qualidade das quadras.</li>
                <li><strong>Suporte dedicado:</strong> Nossa equipe está sempre pronta para ajudar em qualquer dúvida ou dificuldade que você tenha.</li>
                <li><strong>Descontos exclusivos:</strong> Ao realizar seu cadastro, você tem acesso a promoções especiais e descontos em quadras.</li>
                <li><strong>Plataforma fácil de usar:</strong> Nossa interface é intuitiva, sem complicações, para que você foque no que realmente importa: o esporte!</li>
            </ul>

            <div class="historia-imagem-container">
                <img src="../public/shshshshs.webp" alt="Imagem ilustrativa de quadra de esporte" class="historia-imagem">
                <p class="historia-texto-imagem">
                    As imagens das quadras em nossa plataforma são reais e representam fielmente o local de sua próxima reserva.
                </p>
            </div>

            <button class="historia-botao" @click="redirectToRegister">Cadastre-se agora e comece a reservar suas quadras!</button>
        </div>
    </section>
</template>

<script setup>
import { useRouter } from 'vue-router';

const router = useRouter();

function redirectToRegister() {
    router.push('/cadastrar');
}
</script>
<style>
@import url(../assets/Historia.css);
</style>