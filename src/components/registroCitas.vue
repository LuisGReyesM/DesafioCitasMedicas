<template>
    <div class="form-container">
      <!-- Formulario para registro de citas medicas -->
      <form @submit.prevent="registrarCita">
        <h2>Registro de citas médicas</h2>
        <div class="form-row">

          <!-- En los label, se genera para enlazar a dinamicamente clases CSS 
           cuando todos los campos esten llenos cambiará de color -->
          <div class="input-group">
            <label for="paciente" :class="{'label-red': !todosCamposLlenos}">Paciente</label>
            <input id="paciente" v-model="paciente" type="text" />
          </div>
          <div class="input-group">
            <label for="fecha" :class="{'label-red': !todosCamposLlenos}">Fecha</label>
            <input id="fecha" v-model="fecha" type="date" />
          </div>
          <div class="input-group">
            <label for="hora" :class="{'label-red': !todosCamposLlenos}">Hora</label>
            <input id="hora" v-model="hora" type="time" />
          </div>
          <div class="input-group">
            <label for="gravedad" :class="{'label-red': !todosCamposLlenos}">Gravedad</label>
            <select id="gravedad" v-model="gravedad">
              <option value="">Seleccione gravedad</option>
              <option value="baja">Baja</option>
              <option value="media">Media</option>
              <option value="alta">Alta</option>
            </select>
          </div>
          <div class="input-group">
            <label for="motivo" :class="{'label-red': !todosCamposLlenos}">Motivo</label>
            <input id="motivo" v-model="motivo" type="text" />
          </div>
        </div>
        <div class="button-row">
          <!-- Se habilita cuando todosCamposLlenos sea true -->
          <button type="submit" :disabled="!todosCamposLlenos">Agregar</button>
          <button type="button" @click="limpiarCampos">Limpiar</button>
        </div>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        paciente: "",
        fecha: "",
        hora: "",
        gravedad: "",
        motivo: "",
      };
    },
    computed: {      
      todosCamposLlenos() {
        return (
          this.paciente &&
          this.fecha &&
          this.hora &&
          this.gravedad &&
          this.motivo
        );
      },
    },
    methods: {
      registrarCita() {
        if (this.todosCamposLlenos) {
          const nuevaCita = {
            paciente: this.paciente,
            fecha: this.fecha,
            hora: this.hora,
            gravedad: this.gravedad,
            motivo: this.motivo,
          };
          this.$emit("cita-registrada", nuevaCita);
          this.limpiarCampos();
        } 
      },
      limpiarCampos() {
        this.paciente = "";
        this.fecha = "";
        this.hora = "";
        this.gravedad = "";
        this.motivo = "";
      },
    },
  };
  </script>
  
  <style scoped>
  .form-container {
    border: 1px solid #ccc;
    border-radius: 10px;
    padding: 20px;
    margin: 20px auto;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    background-color: #f9f9f9;
  }
  
  form {
    display: flex;
    flex-direction: column;
  }
  
  .form-row {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    margin-bottom: 15px;
  }
  
  .input-group {
    display: flex;
    flex-direction: column;
    flex: 1;
    margin-right: 10px;
  }
  
  .input-group:last-child {
    margin-right: 0;
  }
  
  label {
    margin-bottom: 5px;
  }
  
  .label-red {
    color: red;
    font-weight: bold;
  }
  
  input,
  select {
    padding: 8px;
    font-size: 16px;
  }
  
  .button-row {
    display: flex;
    justify-content: center;
    margin-top: 20px;
  }
  
  button {
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
    margin: 0 10px;
  }
  
  h2 {
    text-align: center;
    margin-bottom: 20px;
  }
  </style>
  