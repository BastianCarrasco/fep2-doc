<script setup>
import { ref, onMounted } from 'vue';

const capituloData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/bt-capitulo-2-antecedentes.json'); // Asegúrate que la ruta sea correcta
        capituloData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Capítulo 2 (Bases Técnicas):', error);
        errorMessage.value = 'No se pudo cargar la información del Capítulo 2 (Bases Técnicas).';
    }
});
</script>

<template>
    <div class="capitulo-container">
        <h1 class="main-title" v-if="capituloData">{{ capituloData.titulo_capitulo }}</h1>

        <div v-if="capituloData" class="content">
            <h2 v-if="capituloData.seccion" class="section-title">{{ capituloData.seccion }}</h2>
            <p v-for="(parrafo, index) in capituloData.parrafos_historia" :key="index">{{ parrafo }}</p>

            <div v-if="capituloData.cifras_actuales" class="sub-section">
                <h3 class="subsection-title">{{ capituloData.cifras_actuales.introduccion }}</h3>
                <ul class="styled-list">
                    <li v-for="(punto, index) in capituloData.cifras_actuales.puntos" :key="index">{{ punto }}</li>
                </ul>
                <p>{{ capituloData.cifras_actuales.paradoja }}</p>
            </div>

            <div v-if="capituloData.fragmentacion_tecnologica" class="sub-section">
                <h3 class="subsection-title">{{ capituloData.fragmentacion_tecnologica.introduccion }}</h3>
                <ul class="styled-list">
                    <li v-for="(punto, index) in capituloData.fragmentacion_tecnologica.puntos" :key="index">{{ punto }}
                    </li>
                </ul>
                <p>{{ capituloData.fragmentacion_tecnologica.cita_munoz }}</p>
            </div>

            <p v-if="capituloData.crisis_sistemica">{{ capituloData.crisis_sistemica }}</p>
            <p v-if="capituloData.punto_inflexion">{{ capituloData.punto_inflexion }}</p>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Capítulo 2: Antecedentes (Bases Técnicas)"...</p>
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

.section-title {
    color: #0056b3;
    margin-top: 35px;
    margin-bottom: 20px;
    font-size: 1.9em;
    font-weight: bold;
    border-left: 4px solid #007bff;
    padding-left: 15px;
}

.sub-section {
    margin-top: 30px;
    margin-bottom: 30px;
    border-left: 2px solid #e0e0e0;
    padding-left: 15px;
}

.subsection-title {
    color: #4a4a4a;
    margin-top: 20px;
    margin-bottom: 10px;
    font-size: 1.5em;
    font-weight: 600;
}

p {
    margin-bottom: 15px;
    text-align: justify;
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