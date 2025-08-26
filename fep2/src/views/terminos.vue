<script setup>
import { ref, onMounted } from 'vue';

const terminosData = ref(null); // Cambiado a terminosData
const errorMessage = ref('');

onMounted(async () => {
    try {
        // Asegúrate de que el nombre del archivo JSON coincida aquí.
        const response = await import('../textos/terminos.json'); // Ruta ajustada
        terminosData.value = response.default;
    } catch (error) {
        console.error('Error al cargar la sección "Términos y definiciones":', error);
        errorMessage.value = 'No se pudo cargar la información de "Términos y definiciones".';
    }
});

// `renderPoints` no es necesaria para la estructura de este JSON, pero se puede quitar.
// Si la dejas, no tendrá efecto si no la usas en el template.
</script>

<template>
    <div class="terminos-container"> <!-- Clase de contenedor específica -->
        <h1 class="main-title" v-if="terminosData">{{ terminosData.titulo_seccion }}</h1>

        <div v-if="terminosData" class="terminos-content">
            <!-- Introducción de la sección -->
            <div class="section-block">
                <p>{{ terminosData.introduccion }}</p>
            </div>

            <!-- Lista de Términos y Definiciones -->
            <div class="section-block">
                <ul class="styled-list terminos-list"> <!-- Nueva clase para estilizar específicamente esta lista -->
                    <li v-for="termino in terminosData.terminos" :key="termino.numero">
                        <strong>{{ termino.numero }} {{ termino.termino }}:</strong> {{ termino.definicion }}
                    </li>
                </ul>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Términos y definiciones"...</p>
    </div>
</template>

<style scoped>
/* Copia y pega los estilos generales del `alcance-container` aquí. */
/* Asegúrate de cambiar la clase principal de `.alcance-container` a `.terminos-container`. */

.terminos-container {
    /* Renombrado para este componente específico */
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

/* La mayoría de las otras clases como .section-block, p, strong, etc., pueden ser las mismas */
/* Si necesitas estilos muy específicos para la lista de términos, puedes usar `.terminos-list` */
.section-block {
    margin-bottom: 30px;
    border-left: 3px solid #e0e0e0;
    padding-left: 15px;
}

p {
    margin-bottom: 10px;
}

strong {
    color: #222;
}

.styled-list {
    list-style: none;
    /* Quitamos el estilo de disco predeterminado */
    margin-left: 0;
    /* Ajustamos la indentación */
    margin-bottom: 15px;
    padding-left: 0;
}

.styled-list li {
    margin-bottom: 12px;
    /* Más espacio entre cada término */
    line-height: 1.5;
    color: #555;
    position: relative;
    padding-left: 25px;
    /* Espacio para el nuevo bullet */
}

.styled-list li::before {
    content: '•';
    /* Un bullet personalizado */
    position: absolute;
    left: 0;
    color: #007bff;
    /* Color del bullet */
    font-size: 1.2em;
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