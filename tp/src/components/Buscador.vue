<template>
  <div class="container-fluid mt-3">
    <div class="form-group">
      <input
        type="text"
        class="form-control"
        v-model="criterioDeBusqueda.nombre"
        placeholder="Buscar por nombre..."
        :disabled="criterioDeBusqueda.dni.length >= 3"
      />
    </div>

    <div class="form-group">
      <input
        type="text"
        class="form-control"
        v-model="criterioDeBusqueda.dni"
        placeholder="Buscar por DNI..."
        :disabled="criterioDeBusqueda.nombre.length >= 3"
      />
    </div>

    <div v-if="mostrarAdvertencia" class="alert alert-warning">
      Debes ingresar al menos 3 caracteres en alguno de los filtros.
    </div>

    <div class="card-deck m-0">
      <div class="row">
        <div class="col" v-for="persona in filtrarPorNombre" :key="persona.dni">
          <div class="card mb-3">
            <div class="card-body">
              <h5 class="card-title">{{ getNombreCompleto(persona) }}</h5>
              <p class="card-text">dni {{ persona.dni }}</p>
              <a href="#" class="card-link">{{ persona.correo }}</a>
            </div>
          </div>
        </div>

        <div class="col" v-for="persona in filtrarPorDni" :key="persona.dni">
          <div class="card mb-3">
            <div class="card-body">
              <h5 class="card-title">{{ getNombreCompleto(persona) }}</h5>
              <p class="card-text">dni {{ persona.dni }}</p>
              <a href="#" class="card-link">{{ persona.correo }}</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      criterioDeBusqueda: {
        nombre: "",
        dni: "",
      },
      personas: [
        {
          nombre: "Daniel",
          apellido: "Sanchez",
          correo: "danielsanchez68@hotmail.com",
          dni: "20442873",
        },
        {
          nombre: "Juan",
          apellido: "Perez",
          correo: "j@p.gmail.com",
          dni: "12345678",
        },
        {
          nombre: "Ana",
          apellido: "Suarez",
          correo: "a@s.gmail.com",
          dni: "87654321",
        },
        {
          nombre: "Carlos",
          apellido: "Mendez",
          correo: "carlosmendez@domain.com",
          dni: "11223344",
        },
      ],
    };
  },
  computed: {
    filtrarPorNombre() {
      if (this.criterioDeBusqueda.nombre.length < 3) return [];
      
      return this.personas.filter((persona) => {
        let registroCompleto = `${persona.nombre} ${persona.apellido}`;
        return registroCompleto
          .toLowerCase()
          .includes(this.criterioDeBusqueda.nombre.toLowerCase());
      });
    },
    filtrarPorDni() {
      if (this.criterioDeBusqueda.dni.length < 3) return [];
      
      return this.personas.filter((persona) => {
        return persona.dni.includes(this.criterioDeBusqueda.dni);
      });
    },
    mostrarAdvertencia() {
      return this.criterioDeBusqueda.nombre.length < 3 && this.criterioDeBusqueda.dni.length < 3;
    },
  },
  methods: {
    getNombreCompleto(persona) {
      return `${persona.nombre} ${persona.apellido}`;
    },
  },
};
</script>

<style scoped>
</style>
