<style scoped>
@import url(../assets/navbar.css);
</style>

<template>

<header class="cabecalho">
        <nav class="cabecalho_menu">
            <img class="cabecalho_menu_logo" src="../public/logo-navbar.png" alt="" width="160px">
            <NuxtLink class="cabecalho_menu_link" to="/">Home <i class="fa-solid fa-house"></i></NuxtLink>
            <NuxtLink class="cabecalho_menu_link" to="/quadras">Quadras <i class="fa-solid fa-globe"></i></NuxtLink>
            <NuxtLink class="cabecalho_menu_link" to="">Quem Somos <i class="fa-solid fa-question"></i></NuxtLink>
            <NuxtLink class="cabecalho_menu_link_login" to="/login">Login/Área Exclusiva <i class="fa-solid fa-user"></i></NuxtLink>
        </nav>
    </header>


</template>