<script setup>
import { ref, onMounted } from 'vue';

const formData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/formulario-t15-plan-de-trabajos-nivelacion-recursos.json'); // Asegúrate que la ruta sea correcta
        formData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Formulario T-15:', error);
        errorMessage.value = 'No se pudo cargar la información del Formulario T-15.';
    }
});
</script>

<template>
    <div class="formulario-container">
        <h1 class="main-title" v-if="formData">{{ formData.titulo_formulario }}</h1>
        <h2 class="sub-title" v-if="formData">{{ formData.subtitulo }}</h2>

        <div v-if="formData" class="content">
            <p v-if="formData.proponente_info" class="proponente-info">{{ formData.proponente_info }}</p>
            <p v-if="formData.instruccion_general" class="form-instruction">{{ formData.instruccion_general }}</p>

            <div v-if="formData.extracto_indicaciones" class="extracto-indicaciones">
                <h3 class="subsection-title">{{ formData.extracto_indicaciones.titulo }}</h3>
                <p v-if="formData.extracto_indicaciones.introduccion">{{ formData.extracto_indicaciones.introduccion }}
                </p>
                <ul v-if="formData.extracto_indicaciones.puntos_resumen" class="styled-list">
                    <li v-for="(punto, index) in formData.extracto_indicaciones.puntos_resumen" :key="index">{{ punto }}
                    </li>
                </ul>
                <p v-if="formData.extracto_indicaciones.programa_trabajos">{{
                    formData.extracto_indicaciones.programa_trabajos }}</p>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Formulario T-15"...</p>
    </div>
</template>

<style scoped>
/* Reutiliza estilos generales de formulario, ajustando si es necesario */
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

.proponente-info {
    font-weight: bold;
    margin-top: 30px;
    margin-bottom: 20px;
    text-align: left;
}

.form-instruction {
    font-style: italic;
    color: #555;
    margin-bottom: 20px;
    text-align: justify;
}

.extracto-indicaciones {
    margin-top: 30px;
    border-left: 3px solid #ccc;
    padding-left: 15px;
}

.subsection-title {
    color: #4a4a4a;
    margin-top: 20px;
    margin-bottom: 10px;
    font-size: 1.4em;
    font-weight: bold;
}

p {
    margin-bottom: 10px;
    text-align: justify;
}

strong {
    color: #222;
}

.styled-list {
    list-style: none;
    /* Quitamos el estilo de disco predeterminado */
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
    content: '▪';
    /* Usando un cuadrado para los puntos del resumen */
    position: absolute;
    left: 0;
    color: #007bff;
    font-size: 1em;
    top: 0;
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