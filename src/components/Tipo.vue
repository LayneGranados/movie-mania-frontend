<template>
  <div>
    <div class="add-book">
      <h4 class="center-align grey-text darken-3">Agregar o Editar Tipo</h4>
      <form>
        <div class="field title">
          <label for="id">Id:</label>
          <input type="text" id="id" v-model="formulario.id" readonly />
        </div>
        <div class="field title">
          <label for="nombre">Nombre:</label>
          <input placeholder="Ingrese el nombre del Tipo" type="text" id="nombre" v-model="formulario.nombre" />
        </div>
        <div class="field title">
          <label for="descripcion">Descripción:</label>
          <input placeholder="Ingrese la descripción del Tipo" type="text" id="descripcion" v-model="formulario.descripcion" />
        </div>
        <div class="field center-align">
          <button class="btn green" @click="guardarTipo">Guardar</button>
          <button class="btn green" @click="editarTipo">Editar</button>
          <button class="btn green" @click="limpiarFormulario">Limpiar</button>
        </div>
      </form>
    </div>
  
    <div class="index container">
      <table>
        <thead>
          <tr>
            <th></th>
            <th>Id</th>
            <th>Nombre</th>
            <th>Descripción</th>
            <th>Fecha de Creación</th>
            <th>Fecha de Actualización</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in lista" :key="item.id">
            <td>
              <input type="checkbox" v-model="item.seleccionado" />
            </td>
            <td>{{ item.id }}</td>
            <td>{{ item.nombre }}</td>
            <td>{{ item.descripcion }}</td>
            <td>{{ item.fechaCreacion }}</td>
            <td>{{ item.fechaActualizacion }}</td>
            <td>
              <button class="btn green" @click="seleccionarTipo(item.id)">Seleccionar</button>
            </td>
            <td>
              <button class="btn green" @click="eliminarTipo(item.id)">Eliminar</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formulario: {
        id: '',
        nombre: '',
        descripcion: '',
        fechaCreacion: '',
        fechaActualizacion: '',
      },
      lista: [],
    };
  },
  mounted() {
    this.obtenerTipos();
  },
  methods: {
    obtenerTipos() {
      fetch('http://localhost:3000/tipos')
        .then(response => response.json())
        .then(data => {
          this.lista = data;
        })
        .catch(error => {
          console.error(error);
        });
    },

    obtenerTipo(id) {
      fetch(`http://localhost:3000/tipos/${id}`)
        .then(response => response.json())
        .then(data => {
          this.formulario = data;
        })
        .catch(error => {
          console.error(error);
        });
    },

    guardarTipo() {
      const tipo = {
        nombre: this.formulario.nombre,
        descripcion: this.formulario.descripcion,
      };

      const requestOptions = {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(tipo),
      };

      fetch('http://localhost:3000/tipos', requestOptions)
        .then(response => response.json())
        .then(data => {
          this.lista.push(data);
          this.limpiarFormulario();
        })
        .catch(error => {
          console.error(error);
        });
    },

    editarTipo() {
      const id = this.formulario.id;

      const tipo = {
        nombre: this.formulario.nombre,
        descripcion: this.formulario.descripcion,
      };

      const requestOptions = {
        method: 'PUT',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(tipo),
      };

      fetch(`http://localhost:3000/tipos/${id}`, requestOptions)
        .then(response => response.json())
        .then(data => {
          const index = this.lista.findIndex(item => item.id === id);
          if (index !== -1) {
            this.lista[index] = data;
          }
          this.limpiarFormulario();
        })
        .catch(error => {
          console.error(error);
        });
    },

    seleccionarTipo(id) {
      this.obtenerTipo(id);
    },

    eliminarTipo(id) {
      fetch(`http://localhost:3000/tipos/${id}`, { method: 'DELETE' })
        .then(() => {
          this.lista = this.lista.filter(item => item.id !== id);
          this.limpiarFormulario();
        })
        .catch(error => {
          console.error(error);
        });
    },

    limpiarFormulario() {
      this.formulario.id = '';
      this.formulario.nombre = '';
      this.formulario.descripcion = '';
      this.formulario.fechaCreacion = '';
      this.formulario.fechaActualizacion = '';

      this.lista.forEach(item => {
        item.seleccionado = false;
      });
    },
  },
};
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}

th,
td {
  padding: 8px;
  border-bottom: 1px solid #ccc;
  text-align: left;
}

button {
  margin-right: 5px;
}
</style>

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

.material-icons {
  margin-right: 30px;
}
.edit {
  cursor: pointer;
  color: pink;
}

.delete {
  cursor: pointer;
  color: red;
}
</style>
