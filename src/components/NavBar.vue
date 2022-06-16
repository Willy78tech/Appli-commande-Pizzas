<template>
  <header>
    <nav class="d-inline-flex mt-2 mt-md-0 ms-md-auto">
    <!-- 
      Ajouter les liens pour les 2 menus
      utiliser les classes class="me-3 py-2 px-3" pour le style
      -->
    <router-link :to="{ name: 'home' }" class="me-3 py-2" >
        Accueil
      </router-link>
      <router-link :to="{ name: 'Contact' }" class="me-3 py-2 px-3" >
        Contact
      </router-link>
    </nav>
  </header>
</template>

<style scoped>
a:active, a:hover, a:visited, a:link {
  color: #fff !important;
  text-decoration: none;
}
a.router-link-active,
a.router-link-exact-active {
  color: #fff;
  border-bottom: 5px solid rgb(48, 195, 67);
}

header {
  background-color: #537698;
  padding: 20px;
}
</style>
