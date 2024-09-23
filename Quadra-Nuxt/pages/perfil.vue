
[<style scoped>

@import url('../assets/perfil.css');
</style>

<template>

<section class="cards-container">
        <a href="###" class="card">
            <div class="card-header">
                <img src="https://i.redd.it/t32e9rm0j1511.jpg" alt="Foto de Perfil do Cliente" class="perfil-imagem"/>
            </div>
            <div class="card-content">
                
                <p class="card-description">Bahia</p>
            </div>
        </a>
    

    
        <a href="###" class="card">
            <div class="card-header">
                <i class="fa-solid fa-address-card"></i>
            </div>
            <div class="card-content">
                <h2 class="card-title">Meus Dados</h2>
                <p class="card-description">Confira as suas informações aqui.</p>
            </div>
        </a>
    

    

        <nuxt-link to="/historico" class="card"> 
            <div class="card-header">
                <i class="fa-solid fa-clipboard-list"></i>
            </div>
            <div class="card-content">
                <h2 class="card-title">Histórico de Quadras</h2>
                <p class="card-description">Confira o seu histórico aqui.</p>
            </div>
        </nuxt-link>
    


    

    <a href="###" class="card">
            <div class="card-header">
                <i class="fa-solid fa-pager"></i>
            </div>
            <div class="card-content">
                <h2 class="card-title">Pagamento</h2>
                <p class="card-description">Confira o seu pagamento aqui.</p>
            </div>
        </a>


    </section>

   

</template>