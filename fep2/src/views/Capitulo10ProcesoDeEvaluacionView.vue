<script setup>
import { ref, onMounted } from 'vue';

const capituloData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/capitulo-10-proceso-de-evaluacion.json'); // Asegúrate que la ruta sea correcta
        capituloData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Capítulo 10:', error);
        errorMessage.value = 'No se pudo cargar la información del Capítulo 10.';
    }
});
</script>

<template>
    <div class="capitulo-container">
        <h1 class="main-title" v-if="capituloData">{{ capituloData.titulo_capitulo }}</h1>

        <div v-if="capituloData && capituloData.articulos" class="content">
            <div v-for="articulo in capituloData.articulos" :key="articulo.numero" class="article-block">
                <h2 class="article-title">{{ articulo.numero }}: {{ articulo.titulo }}</h2>

                <!-- ARTÍCULO 29°: COMISIÓN EVALUADORA -->
                <template v-if="articulo.numero === 'ARTÍCULO 29°'">
                    <p v-if="articulo.introduccion">{{ articulo.introduccion }}</p>
                    <ul v-if="articulo.atribuciones" class="styled-list">
                        <li v-for="(atribucion, index) in articulo.atribuciones" :key="index">{{ atribucion }}</li>
                    </ul>
                </template>

                <!-- ARTÍCULO 30°: EVALUACIÓN ADMINISTRATIVA -->
                <template v-if="articulo.numero === 'ARTÍCULO 30°'">
                    <p v-if="articulo.introduccion">{{ articulo.introduccion }}</p>
                    <ul v-if="articulo.subsanacion_errores" class="styled-list">
                        <li v-for="(error, index) in articulo.subsanacion_errores" :key="index">{{ error }}</li>
                    </ul>
                    <p v-if="articulo.inadmisibilidad_ofertas" class="important-note">{{
                        articulo.inadmisibilidad_ofertas }}</p>
                </template>

            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Capítulo 10: Proceso de Evaluación"...</p>
    </div>
</template>

<style scoped>
/* Estilos generales del Capítulo */
.capitulo-container {
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

.article-block {
    margin-bottom: 40px;
    border-left: 4px solid #0056b3;
    padding-left: 20px;
}

.article-title {
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