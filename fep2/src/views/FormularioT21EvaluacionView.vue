<script setup>
import { ref, onMounted } from 'vue';

const formData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/formulario-t21-evaluacion.json'); // Asegúrate que la ruta sea correcta
        formData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Formulario T-21:', error);
        errorMessage.value = 'No se pudo cargar la información del Formulario T-21.';
    }
});
</script>

<template>
    <div class="formulario-container">
        <h1 class="main-title" v-if="formData">{{ formData.titulo_formulario }}</h1>
        <h2 class="sub-title" v-if="formData">{{ formData.subtitulo }}</h2>

        <div v-if="formData" class="content">
            <p v-if="formData.introduccion" class="form-instruction">{{ formData.introduccion }}</p>
            <p v-if="formData.evaluacion_por_item">{{ formData.evaluacion_por_item }}</p>
            <p v-if="formData.peso_item">{{ formData.peso_item }}</p>

            <h3 class="subsection-title" v-if="formData.criterios_asignacion_porcentaje">{{
                formData.criterios_asignacion_porcentaje.titulo }}</h3>
            <ul v-if="formData.criterios_asignacion_porcentaje && formData.criterios_asignacion_porcentaje.puntos"
                class="styled-list">
                <li v-for="(punto, index) in formData.criterios_asignacion_porcentaje.puntos" :key="index">{{ punto }}
                </li>
            </ul>

            <p v-if="formData.informacion_detalle" class="form-instruction">{{ formData.informacion_detalle }}</p>

            <h3 class="subsection-title" v-if="formData.ponderacion_evaluacion_contenido">{{
                formData.ponderacion_evaluacion_contenido.titulo }}</h3>
            <div class="table-responsive">
                <table>
                    <thead>
                        <tr>
                            <th v-for="(header, index) in formData.ponderacion_evaluacion_contenido.encabezados"
                                :key="index" v-html="header.replace(/\n/g, '<br>')"></th>
                        </tr>
                    </thead>
                    <tbody>
                        <template v-for="(subdoc, docIndex) in formData.ponderacion_evaluacion_contenido.subdocumentos"
                            :key="docIndex">
                            <tr class="subdocument-header-row">
                                <td colspan="4"><strong>{{ subdoc.titulo }}</strong></td>
                            </tr>
                            <tr v-for="(item, itemIndex) in subdoc.items" :key="itemIndex"
                                :class="{ 'table-header-item': item.type === 'header' }">
                                <td>{{ item.id }} {{ item.descripcion }}</td>
                                <td>{{ item.inf1_peso }}</td>
                                <td>{{ item.inf2_peso }}</td>
                                <td>{{ item.final_peso }}</td>
                            </tr>
                        </template>
                    </tbody>
                </table>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Formulario T-21"...</p>
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
    margin-bottom: 15px;
    text-align: justify;
}

.subsection-title {
    color: #4a4a4a;
    margin-top: 25px;
    margin-bottom: 15px;
    font-size: 1.6em;
    font-weight: bold;
    border-bottom: 1px dashed #eee;
    padding-bottom: 5px;
}

.styled-list {
    list-style: none;
    margin-left: 0;
    margin-bottom: 15px;
    padding-left: 20px;
}

.styled-list li {
    margin-bottom: 8px;
    line-height: 1.5;
    color: #555;
    position: relative;
    padding-left: 10px;
}

.styled-list li::before {
    content: '•';
    position: absolute;
    left: 0;
    color: #007bff;
    font-size: 1em;
    top: 0;
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
    /* Ajusta según el contenido de tu tabla */
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

.subdocument-header-row td {
    background-color: #e6f7ff;
    /* Fondo para el título del subdocumento */
    font-weight: bold;
    color: #0056b3;
    text-transform: uppercase;
    text-align: center;
}

.table-header-item td {
    /* Para ítems que son como encabezados dentro de la tabla */
    font-weight: bold;
    color: #333;
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