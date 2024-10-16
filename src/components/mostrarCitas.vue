<template>
    <div>
        <!-- Mensaje cuando no hay citas -->
        <p v-if="citas.length === 0" class="no-citas">Aún no hay consultas registradas.</p>
        <div class="card-container">
            <div v-for="(cita, index) in citas" :key="index" class="cita-card" :class="{
                'grave': cita.gravedad === 'alta',
                'moderada': cita.gravedad === 'media',
                'leve': cita.gravedad === 'baja'
            }">
                <p><strong>Paciente:</strong></p>
                <p>{{ cita.paciente }}</p>
                <p><strong>Fecha:</strong></p>
                <p>{{ cita.fecha }}</p>
                <p><strong>Hora:</strong></p>
                <p>{{ cita.hora }}</p>
                <p><strong>Gravedad:</strong></p>
                <p>{{ cita.gravedad }}</p>                
                <p><strong>Motivo:</strong></p> 
                    <p>{{ cita.motivo }}</p>
                <button @click="eliminarCita(index)">Eliminar</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        citas: Array,
    },
    methods: {
        eliminarCita(index) {
            this.$emit('eliminar-cita', index); // Emitir un evento para eliminar la cita
        },
    },
};
</script>

<style scoped>
.no-citas {
    color: red;
    /* Color rojo para el mensaje de sin citas */
    font-size: 18px;  
    margin: 20px;  
}

.card-container {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    justify-content: center;
    text-align: center;
}

.cita-card {
    border: 1px solid #ccc;
    padding: 16px;
    margin: 10px;   
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    width: 200px;    
    box-sizing: border-box;   
}

/* Estilos para los colores de gravedad */
.grave {
    background-color: #f8d7da;    
}

.moderada {
    background-color: #fff3cd;  
}

.leve {
    background-color: #d4edda;   
}
</style>
