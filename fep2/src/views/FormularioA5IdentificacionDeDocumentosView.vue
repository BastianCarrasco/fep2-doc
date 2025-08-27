<script setup>
import { ref, onMounted } from 'vue';

const formData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/formulario-a5-identificacion-de-documentos.json'); // Asegúrate que la ruta sea correcta
        formData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Formulario A-5:', error);
        errorMessage.value = 'No se pudo cargar la información del Formulario A-5.';
    }
});
</script>

<template>
    <div class="formulario-container">
        <h1 class="main-title" v-if="formData">{{ formData.titulo_formulario }}</h1>
        <h2 class="sub-title" v-if="formData">{{ formData.subtitulo }}</h2>

        <div v-if="formData && formData.tabla_documentos" class="content">
            <div class="table-responsive">
                <table>
                    <thead>
                        <tr>
                            <th v-for="(header, index) in formData.tabla_documentos.encabezados" :key="index">{{ header
                                }}</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(fila, index) in formData.tabla_documentos.filas" :key="index">
                            <td>
                                <p>{{ fila.antecedente }}</p>
                                <ul v-if="fila.subpuntos" class="styled-list sub-points">
                                    <li v-for="(subpunto, subIndex) in fila.subpuntos" :key="subIndex">{{ subpunto }}
                                    </li>
                                </ul>
                            </td>
                            <td><!-- Columna para "Incluido (SI/NO)" --></td>
                            <td><!-- Columna para "Folio de Hoja" --></td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <div v-if="formData.firma" class="firma-section">
                <p class="firma-line">{{ formData.firma.texto }}</p>
                <p class="firma-label">{{ formData.firma.cargo }}</p>
                <p class="firma-date">{{ formData.firma.lugar_fecha }}</p>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Formulario A-5"...</p>
    </div>
</template>

<style scoped>
/* Copia y pega los estilos generales del Formulario A-1 aquí, ajustando si es necesario */
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

td ul.styled-list.sub-points {
    /* Estilo específico para subpuntos dentro de la celda de la tabla */
    list-style: none;
    margin: 5px 0 0 0;
    padding-left: 15px;
}

td ul.styled-list.sub-points li::before {
    content: '-';
    position: absolute;
    left: 0;
    color: #4a4a4a;
    font-size: 1em;
    top: 0;
}


.firma-section {
    margin-top: 50px;
    text-align: right;
    border-top: 1px solid #eee;
    padding-top: 20px;
}

.firma-line {
    margin: 0;
    font-size: 1.1em;
    font-weight: bold;
    color: #333;
}

.firma-label {
    margin: 5px 0 0 0;
    font-size: 0.9em;
    color: #555;
}

.firma-date {
    margin: 5px 0 0 0;
    font-size: 0.9em;
    color: #555;
    font-style: italic;
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