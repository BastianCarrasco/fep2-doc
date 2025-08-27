<script setup>
import { ref, onMounted } from 'vue';

const formData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/formulario-t20-calendario-de-actividades.json'); // Asegúrate que la ruta sea correcta
        formData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Formulario T-20:', error);
        errorMessage.value = 'No se pudo cargar la información del Formulario T-20.';
    }
});
</script>

<template>
    <div class="formulario-container">
        <h1 class="main-title" v-if="formData">{{ formData.titulo_formulario }}</h1>
        <h2 class="sub-title" v-if="formData">{{ formData.subtitulo }}</h2>

        <div v-if="formData" class="content">
            <p v-if="formData.introduccion" class="form-instruction">{{ formData.introduccion }}</p>

            <div class="table-responsive">
                <table>
                    <thead>
                        <tr>
                            <th v-for="(header, index) in formData.calendario_actividades.encabezados" :key="index">{{
                                header }}</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(fila, index) in formData.calendario_actividades.filas" :key="index">
                            <td>{{ fila.nro }}</td>
                            <td>{{ fila.actividad }}</td>
                            <td>{{ fila.fecha_inicio }}</td>
                            <td>{{ fila.fecha_termino }}</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Formulario T-20"...</p>
    </div>
</template>

<style scoped>
/* Reutiliza estilos generales de formulario y tabla, ajustando si es necesario */
.formulario-container {
    padding: 30px;
    background-color: #ffffff;
    border-radius: 8px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
    line-height: 1.6;
    color: #333;
    font-family: Georgia, serif;
}

.main-title {
    color: #1a237e;
    margin-bottom: 5px;
    font-size: 2em;
    font-weight: bold;
    text-align: center;
}

.sub-title {
    color: #007bff;
    margin-bottom: 30px;
    border-bottom: 2px solid #007bff;
    padding-bottom: 10px;
    font-size: 1.5em;
    font-weight: 600;
    text-align: center;
}

.form-instruction {
    font-style: italic;
    color: #555;
    margin-bottom: 20px;
    text-align: justify;
}

.table-responsive {
    overflow-x: auto;
    margin-top: 20px;
    margin-bottom: 30px;
}

table {
    width: 100%;
    border-collapse: collapse;
    min-width: 600px;
}

th,
td {
    border: 1px solid #e0e0e0;
    padding: 12px 15px;
    text-align: left;
    vertical-align: top;
    font-size: 0.9em;
}

th {
    background-color: #f5f7fa;
    font-weight: 700;
    color: #333;
    text-transform: uppercase;
}

tbody tr:nth-child(even) {
    background-color: #fcfdff;
}

tbody tr:hover {
    background-color: #eef7ff;
}

.loading-message,
.error-message {
    text-align: center;
    padding: 20px;
    font-size: 1.1em;
    border-radius: 5px;
    margin-top: 20px;
}

.loading-message {
    background-color: #e6f7ff;
    color: #0056b3;
}

.error-message {
    background-color: #ffebeb;
    color: #cc0000;
    border: 1px solid #ff0000;
}
</style>