<script setup>
import { ref, onMounted } from 'vue';

const formData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/formulario-t22-contenido-presentaciones-preparatorias.json'); // Asegúrate que la ruta sea correcta
        formData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Formulario T-22:', error);
        errorMessage.value = 'No se pudo cargar la información del Formulario T-22.';
    }
});
</script>

<template>
    <div class="formulario-container">
        <h1 class="main-title" v-if="formData">{{ formData.titulo_formulario }}</h1>
        <h2 class="sub-title" v-if="formData">{{ formData.subtitulo }}</h2>

        <div v-if="formData" class="content">
            <div v-if="formData.propuesta_presentaciones" class="section-block">
                <p v-if="formData.propuesta_presentaciones.introduccion" class="form-instruction">
                    {{ formData.propuesta_presentaciones.introduccion }}
                </p>
                <p v-if="formData.propuesta_presentaciones.obligatoriedad" class="form-instruction important-note">
                    {{ formData.propuesta_presentaciones.obligatoriedad }}
                </p>
            </div>

            <!-- Informe y Presentación 1 -->
            <div v-if="formData.informe_presentacion_1" class="section-block">
                <h3 class="subsection-title">{{ formData.informe_presentacion_1.titulo }}</h3>
                <ul v-if="formData.informe_presentacion_1.puntos_contenido" class="styled-list">
                    <li v-for="(punto, index) in formData.informe_presentacion_1.puntos_contenido" :key="index">
                        {{ punto.contenido }}
                    </li>
                </ul>
                <template v-if="formData.informe_presentacion_1.corresponde_propuesta_tecnica">
                    <p class="sub-section-intro">
                        <strong>{{ formData.informe_presentacion_1.corresponde_propuesta_tecnica.titulo }}</strong>
                    </p>
                    <ul class="styled-list sub-points">
                        <li v-for="(doc, index) in formData.informe_presentacion_1.corresponde_propuesta_tecnica.subdocumentos"
                            :key="index">{{ doc }}</li>
                    </ul>
                </template>
            </div>

            <!-- Informe y Presentación 2 -->
            <div v-if="formData.informe_presentacion_2" class="section-block">
                <h3 class="subsection-title">{{ formData.informe_presentacion_2.titulo }}</h3>
                <ul v-if="formData.informe_presentacion_2.puntos_contenido" class="styled-list">
                    <li v-for="(punto, index) in formData.informe_presentacion_2.puntos_contenido" :key="index">
                        {{ punto.contenido }}
                    </li>
                </ul>
                <template v-if="formData.informe_presentacion_2.corresponde_propuesta_tecnica">
                    <p class="sub-section-intro">
                        <strong>{{ formData.informe_presentacion_2.corresponde_propuesta_tecnica.titulo }}</strong>
                    </p>
                    <ul class="styled-list sub-points">
                        <li v-for="(doc, index) in formData.informe_presentacion_2.corresponde_propuesta_tecnica.subdocumentos"
                            :key="index">{{ doc }}</li>
                    </ul>
                </template>
            </div>

            <!-- Informe y Presentación 3 -->
            <div v-if="formData.informe_presentacion_3" class="section-block">
                <h3 class="subsection-title">{{ formData.informe_presentacion_3.titulo }}</h3>
                <ul v-if="formData.informe_presentacion_3.puntos_contenido" class="styled-list">
                    <li v-for="(punto, index) in formData.informe_presentacion_3.puntos_contenido" :key="index">
                        {{ punto.contenido }}
                    </li>
                </ul>
                <p v-if="formData.informe_presentacion_3.informacion_adicional" class="form-instruction">
                    {{ formData.informe_presentacion_3.informacion_adicional }}
                </p>
                <p v-if="formData.informe_presentacion_3.propuesta_economica_final" class="form-instruction">
                    {{ formData.informe_presentacion_3.propuesta_economica_final }}
                </p>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Formulario T-22"...</p>
    </div>
</template>

<style scoped>
/* Reutiliza estilos generales de formulario */
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

.important-note {
    font-weight: bold;
    color: #d9534f;
    /* Un color de advertencia */
    margin-top: 20px;
    margin-bottom: 20px;
    padding: 10px 15px;
    border: 1px solid #d9534f;
    border-radius: 5px;
    background-color: #fdf7f7;
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

.sub-section-intro {
    font-weight: bold;
    margin-top: 15px;
    margin-bottom: 5px;
    color: #333;
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

.styled-list.sub-points li::before {
    content: '-';
    /* Para los puntos de subdocumentos */
    color: #4a4a4a;
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