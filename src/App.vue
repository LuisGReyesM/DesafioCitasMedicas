<template>
  <div class="container">
    <div class="registro-cita">
      <!-- Componente de registro de citas médicas -->
      <Registro @cita-registrada="agregarCita" />
    </div>
    <div class="lista-citas-container">
      <!-- Componente para mostrar las citas en forma de tarjetas -->
      <Listar :citas="citas" @eliminar-Cita="eliminarCita" />
    </div>
  </div>
</template>

<script>
import Registro from "./components/registroCitas.vue";
import Listar from "./components/mostrarCitas.vue";

export default {
  components: {
    Registro,
    Listar,
  },
  data() {
    return {
      citas: [],
    };
  },
  methods: {
    // Método para agregar una nueva cita
    agregarCita(nuevaCita) {
      this.citas.push(nuevaCita);
    },
    // Método para eliminar una cita
    eliminarCita(index) {
      this.citas.splice(index, 1);
    },
  },
};
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.lista-citas-container {
  width: 100%;
  margin-top: 20px;
  display: flex;
  flex-wrap: wrap; 
  justify-content: center;
  gap: 20px; 
}
.detalle-usuario {
  text-align: center;
}
</style>
