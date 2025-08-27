<script setup>
import { ref, onMounted } from 'vue';

const anexoData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/anexo-a-volumetria-actual-y-proyectada.json'); // Asegúrate que la ruta sea correcta
        anexoData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Anexo A:', error);
        errorMessage.value = 'No se pudo cargar la información del Anexo A.';
    }
});
</script>

<template>
    <div class="anexo-container">
        <h1 class="main-title" v-if="anexoData">{{ anexoData.titulo_anexo }}</h1>

        <div v-if="anexoData && anexoData.secciones" class="content">
            <div v-for="(seccion, index) in anexoData.secciones" :key="index" class="section-block">
                <h2 class="section-title">{{ seccion.titulo }}</h2>
                <ul v-if="seccion.puntos" class="styled-list">
                    <li v-for="(punto, pIndex) in seccion.puntos" :key="pIndex">{{ punto }}</li>
                </ul>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Anexo A: Volumetría Actual y Proyectada"...</p>
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

.section-block {
    margin-bottom: 40px;
    border-left: 4px solid #0056b3;
    padding-left: 20px;
}

.section-title {
    color: #0056b3;
    margin-top: 35px;
    margin-bottom: 15px;
    font-size: 1.9em;
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