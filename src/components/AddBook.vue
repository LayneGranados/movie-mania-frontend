<template>
  <div class="add-book">
    <h4 class="center-align grey-text darken-3">Agrega Pelicula, Serie, Documental</h4>
    <form @submit.prevent="addBook">
      <div class="field title">
        <label for="nombre">Nombre:</label>
        <input type="text" name="nombre" v-model="nombre" />
      </div>
      <div class="field title">
        <label for="fecha">Fecha Publicacion:</label>
        <input type="date" name="fecha" v-model="fecha" />
      </div>
      <div class="">
        <label for="estado">Estado:</label>
        <select name="estado" v-model="estado" class="browser-default">
          <option value="Activo">Activo</option>
          <option value="Inactivo">Inactivo</option>
          <option value="Indefinido">Indefinido</option>
        </select>
      </div>
      <div class="field title">
        <label for="link">Link:</label>
        <input type="text" name="link" v-model="link" />
      </div>
      <div class="field title">
        <label for="genero">Género:</label>
        <select name="genero" v-model="genero" class="browser-default">
          <option v-for="item in generos" :key="item.id" :value="item.nombre">{{ item.nombre }}</option>
        </select>
      </div>
      <div class="field title">
        <label for="tipo">Tipo:</label>
        <select name="tipo" v-model="tipo" class="browser-default">
          <option v-for="item in tipos" :key="item.id" :value="item.nombre">{{ item.nombre }}</option>
        </select>
      </div>
      <div class="field title">
        <label for="plataforma">Plataforma:</label>
        <select name="plataforma" v-model="plataforma" class="browser-default">
          <option v-for="item in plataformas" :key="item.id" :value="item.nombre">{{ item.nombre }}</option>
        </select>
      </div>
      <div class="field center-align">
        <button class="btn green">Add Recurso</button>
      </div>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      nombre: '',
      fecha: '',
      estado: '',
      link: '',
      generos: [],
      tipos: [],
      plataformas: []
    };
  },
  mounted() {
    this.obtenerGeneros();
    this.obtenerTipos();
    this.obtenerPlataformas();
  },
  methods: {
    addBook() {
      const bookData = {
        nombre: this.nombre,
        fecha: this.fecha,
        estado: this.estado,
        link: this.link,
        genero: this.genero,
        tipo: this.tipo,
        plataforma: this.plataforma
      };

      axios
        .post('http://localhost:3000/agregar-recurso', bookData)
        .then(response => {
          console.log(response);
        })
        .catch(error => {
          console.error('Error al agregar el recurso:', error);
        });
    },
    obtenerGeneros() {
      fetch('http://localhost:3000/generos')
        .then(response => response.json())
        .then(data => {
          this.generos = data;
        })
        .catch(error => {
          console.error(error);
        });
    },
    obtenerTipos() {
      fetch('http://localhost:3000/tipos')
        .then(response => response.json())
        .then(data => {
          this.tipos = data;
        })
        .catch(error => {
          console.error(error);
        });
    },
    obtenerPlataformas() {
      fetch('http://localhost:3000/plataformas')
        .then(response => response.json())
        .then(data => {
          this.plataformas = data;
        })
        .catch(error => {
          console.error(error);
        });
    }
  }
};
</script>

<style>
.add-book {
  max-width: 700px;
  margin: 0 auto;
}

.add-book form {
  padding: 30px;
}

.add-book .btn {
  margin-top: 30px;
}
</style>
