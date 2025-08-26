<script setup>
import { ref, onMounted } from 'vue';

const alcanceData = ref(null); // Cambiado a alcanceData
const errorMessage = ref('');

onMounted(async () => {
    try {
        // Asegúrate de que el nombre del archivo JSON coincida aquí.
        const response = await import('../textos/alcance-y-campo-de-aplicacion.json'); // Ruta ajustada
        alcanceData.value = response.default;
    } catch (error) {
        console.error('Error al cargar la sección "Alcance y campo de aplicación":', error);
        errorMessage.value = 'No se pudo cargar la información de "Alcance y campo de aplicación".';
    }
});

// Esta función `renderPoints` ya no sería necesaria para este JSON simplificado,
// pero la dejo por si la necesitas para futuros JSON con estructuras similares a la introducción.
const renderPoints = (points) => {
    if (!points || points.length === 0) return null;
    return points.map(p => {
        let text = p.item || p.definicion;
        if (p.letra) {
            text = p.letra + ' ' + text;
        }
        return text;
    }).filter(Boolean);
};
</script>

<template>
    <div class="alcance-container"> <!-- Cambiado a alcance-container para estilos específicos si es necesario -->
        <h1 class="main-title" v-if="alcanceData">{{ alcanceData.titulo_seccion }}</h1>

        <div v-if="alcanceData" class="alcance-content">
            <!-- Sección: Introducción -->
            <div class="section-block">
                <p>{{ alcanceData.introduccion }}</p>
            </div>

            <!-- Sección: Alcance y aplicabilidad -->
            <div class="section-block">
                <h2 class="section-title">Alcance y aplicabilidad</h2>
                <p>{{ alcanceData.alcance_y_aplicabilidad.descripcion }}</p>
                <h3 class="subsection-title">{{ alcanceData.alcance_y_aplicabilidad.factores_considerar }}</h3>
                <ul class="styled-list">
                    <li v-for="(factor, index) in alcanceData.alcance_y_aplicabilidad.puntos_factores" :key="index">
                        {{ factor }}
                    </li>
                </ul>
                <p>{{ alcanceData.alcance_y_aplicabilidad.no_especifica }}</p>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Alcance y campo de aplicación"...</p>
    </div>
</template>

<style scoped>
/* **Importante:** Copia los estilos de `.preambulo-container` de tu `PreambuloView.vue` aquí. */
/* Asegúrate de ajustar `.intro-container` a `.alcance-container` si cambiaste la clase en el template. */
/* Si deseas, puedes mantener el nombre de clase `intro-container` para los estilos si todas las vistas comparten el mismo contenedor principal. */

.alcance-container {
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

.section-title {
    color: #007bff;
    margin-top: 40px;
    margin-bottom: 20px;
    font-size: 1.8em;
    font-weight: bold;
    position: relative;
    padding-left: 15px;
}

.section-title::before {
    content: '▪';
    position: absolute;
    left: 0;
    color: #007bff;
    font-size: 1.2em;
    top: 50%;
    transform: translateY(-50%);
}

.section-block {
    margin-bottom: 30px;
    border-left: 3px solid #e0e0e0;
    padding-left: 15px;
}

.subsection-title {
    color: #4a4a4a;
    margin-top: 25px;
    margin-bottom: 10px;
    font-size: 1.4em;
    font-weight: 600;
}

p {
    margin-bottom: 10px;
}

strong {
    color: #222;
}

.styled-list {
    list-style: disc;
    margin-left: 25px;
    margin-bottom: 15px;
    padding-left: 0;
}

.styled-list li {
    margin-bottom: 8px;
    line-height: 1.5;
    color: #555;
}

.table-responsive {
    /* Aunque no se usa aquí, lo mantengo por si lo necesitas en otras vistas */
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