<template>
    <footer class="rodape">
        <div class="rodape-div">
            <h3 class="rodape-titulo">Contato</h3>
            <div class="rodape-icons">
                <a href="https://wa.me/5516992594" class="icons-links">
                    <i class="fa-solid fa-phone fa-icons"></i>
                </a>
                <a href="mailto:Quadra.Finder@gmail.com" class="icons-links">
                    <i class="fa-solid fa-envelope fa-icons"></i>
                </a>
                <a href="#" class="icons-links">
                    <i class="fa-brands fa-instagram fa-icons"></i>
                </a>
                <a href="#" class="icons-links">
                    <i class="fa-brands fa-twitter fa-icons"></i>
                </a>
                <a href="#" class="icons-links">
                    <i class="fa-brands fa-tiktok fa-icons"></i>
                </a>
            </div>
            <p class="rodape-texto-final">
                ©2024 São Carlos Quadra Finder - Quadras perto de sua Região. Todos os Direitos Reservados. <a href="#" class="rodape-texto-link">Política de Privacidade</a>
            </p>
        </div>
    </footer>
</template>

<style scoped>
.rodape {
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: var(--cor-navbar);
    padding: 20px 0;
}

.rodape-div {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    max-width: 1200px;
    width: 100%;
}

.rodape-titulo {
    font-size: 1.5rem;
    font-weight: bold;
    color: white;
    margin-bottom: 10px;
}

.rodape-icons {
    display: flex;
    justify-content: center;
    margin-bottom: 15px;
}

.icons-links {
    margin: 0 15px;
    transition: transform 0.3s ease;
}

.fa-icons {
    font-size: 1.5rem;
    color: var(--cor-principal);
}

.fa-icons:hover {
    color: var(--cor-secundaria);
    font-size: 1.7rem;
    transform: scale(1.1);
}

.rodape-texto-final {
    font-size: 0.9rem;
    color: white;
    margin-top: 10px;
}

.rodape-texto-link {
    text-decoration: none;
    color: var(--cor-principal);
    font-weight: bold;
}

.rodape-texto-link:hover {
    color: var(--cor-secundaria);
    transition: 0.3s;
}

@media (max-width: 768px) {
    .rodape-icons {
        flex-direction: column;
    }

    .icons-links {
        margin: 10px 0;
    }

    .rodape-texto-final {
        font-size: 0.8rem;
    }
}
</style>
