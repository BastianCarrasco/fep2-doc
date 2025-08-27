<script setup>
import { ref, onMounted } from 'vue';

const anexoData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/anexo-b-definiciones-y-glosario.json'); // Asegúrate que la ruta sea correcta
        anexoData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Anexo B:', error);
        errorMessage.value = 'No se pudo cargar la información del Anexo B.';
    }
});
</script>

<template>
    <div class="anexo-container">
        <h1 class="main-title" v-if="anexoData">{{ anexoData.titulo_anexo }}</h1>

        <div v-if="anexoData && anexoData.definiciones" class="content">
            <ul class="styled-list glosario-list">
                <li v-for="(definicion, index) in anexoData.definiciones" :key="index">
                    <strong>{{ definicion.termino }}:</strong> {{ definicion.definicion }}
                </li>
            </ul>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Anexo B: Definiciones y Glosario"...</p>
    </div>
</template>

<style scoped>
/* Estilos generales para Anexos, puedes reutilizar los de otros capítulos o crear específicos */
.anexo-container {
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
    margin-bottom: 30px;
    border-bottom: 2px solid #007bff;
    padding-bottom: 15px;
    font-size: 2.2em;
    font-weight: bold;
    text-align: center;
}

.glosario-list {
    padding-left: 0;
    /* No indentar extra si ya tienes strong en el inicio */
}

.glosario-list li {
    margin-bottom: 10px;
    line-height: 1.6;
    color: #555;
    padding-left: 0;
}

.glosario-list li strong {
    color: #0056b3;
    /* Color de acento para el término */
    margin-right: 5px;
    min-width: 80px;
    /* Ancho mínimo para alinear, ajustar si es necesario */
    display: inline-block;
}

p {
    margin-bottom: 10px;
    text-align: justify;
}

strong {
    color: #222;
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