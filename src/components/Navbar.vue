<template>
  <div class="navbar">
    <nav class="nav-extended pink darken-3">
      <div class="nav-content">
        <router-link :to="{ name: 'Index' }">
          <span class="nav-title">Películas, series, documentales y más</span>
        </router-link>

        <a href="#" class="btn-floating btn-large halfway-fab green">
          <router-link :to="{ name: 'AddBook' }">
            <i class="material-icons">add</i>
          </router-link>
        </a>
      </div>
    </nav>

    <div class="menu">
      <ul class="pink darken-3">
        <li><router-link :to="{ name: 'Plataforma' }">Plataforma</router-link></li>
        <li><router-link :to="{ name: 'Genero' }">Genero</router-link></li>
        <li><router-link :to="{ name: 'Tipo' }">Tipo</router-link></li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  data() {
    return {};
  }
};
</script>

<style scoped>
.navbar {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.navbar nav {
  padding: 0 30px;
}

.menu {
  background-color: var(--pink-darken-3); /* Mismo color que el navbar */
  position: relative;
}

.menu ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.menu li {
  margin-bottom: 10px;
}

.menu li a {
  text-decoration: none;
  color: white; /* Color de texto blanco */
  font-size: 16px;
}

.menu li a:hover {
  color: #ff4081; /* Color de resaltado al pasar el cursor */
}
</style>
