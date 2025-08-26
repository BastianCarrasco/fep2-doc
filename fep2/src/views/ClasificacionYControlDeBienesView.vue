<script setup>
import { ref, onMounted } from 'vue';

const clasificacionData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textos/clasificacion-y-control-de-bienes.json'); // Ajusta la ruta
        clasificacionData.value = response.default;
    } catch (error) {
        console.error('Error al cargar la sección "Clasificación y control de bienes":', error);
        errorMessage.value = 'No se pudo cargar la información de "Clasificación y control de bienes".';
    }
});
</script>

<template>
    <div class="clasificacion-container">
        <h1 class="main-title" v-if="clasificacionData">{{ clasificacionData.titulo_seccion }}</h1>

        <div v-if="clasificacionData && clasificacionData.secciones" class="content">
            <div v-for="section in clasificacionData.secciones" :key="section.numero" class="section-group">
                <h2 class="section-title">{{ section.numero }} {{ section.titulo }}</h2>
                <p v-if="section.objetivo" class="section-objective">Objetivo: {{ section.objetivo }}</p>
                <p v-if="section.parrafo_introductorio">{{ section.parrafo_introductorio }}</p>
                <p v-if="section.descripcion">{{ section.descripcion }}</p>

                <div v-for="subsection in section.subsecciones" :key="subsection.numero" class="subsection-group">
                    <h3 class="subsection-title">{{ subsection.numero }} {{ subsection.titulo }}</h3>
                    <p v-if="subsection.importancia_inventario">{{ subsection.importancia_inventario }}</p>
                    <p v-if="subsection.implementacion_inventario">{{ subsection.implementacion_inventario }}</p>

                    <!-- Ejemplos de bienes (5.1.1) -->
                    <ul v-if="subsection.ejemplos_bienes" class="styled-list">
                        <li v-for="(bien, index) in subsection.ejemplos_bienes" :key="index">
                            <strong>{{ bien.letra }}</strong> <strong>{{ bien.tipo }}:</strong> {{ bien.ejemplos }}
                        </li>
                    </ul>

                    <p v-if="subsection.consideraciones_clasificacion">{{ subsection.consideraciones_clasificacion }}
                    </p>
                    <p v-if="subsection.etiquetado_valor_sensibilidad">{{ subsection.etiquetado_valor_sensibilidad }}
                    </p>
                    <p v-if="subsection.cambio_clasificacion">{{ subsection.cambio_clasificacion }}</p>
                    <p v-if="subsection.categorias_complejidad">{{ subsection.categorias_complejidad }}</p>
                    <p v-if="subsection.responsabilidad_clasificacion">{{ subsection.responsabilidad_clasificacion }}
                    </p>

                    <!-- Tipos de actividad (5.2.2) -->
                    <p v-if="subsection.introduccion && subsection.numero === '5.2.2'">{{ subsection.introduccion }}</p>
                    <ul v-if="subsection.tipos_actividad" class="styled-list">
                        <li v-for="(actividad, index) in subsection.tipos_actividad" :key="index">
                            <strong>{{ actividad.letra }}</strong> {{ actividad.item }}
                        </li>
                    </ul>
                    <p v-if="subsection.etiquetado_salida">{{ subsection.etiquetado_salida }}</p>
                    <p v-if="subsection.etiquetas_fisicas_electronicas">{{ subsection.etiquetas_fisicas_electronicas }}
                    </p>
                </div>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Clasificación y control de bienes"...</p>
    </div>
</template>

<style scoped>
/* Copia y pega los estilos generales de SeguridadOrganizacionalView.vue aquí. */
/* Renombra la clase principal del contenedor si la cambiaste en el template. */
.clasificacion-container {
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

.section-group {
    margin-bottom: 45px;
    border-left: 4px solid #007bff;
    padding-left: 20px;
}

.section-title {
    color: #007bff;
    margin-top: 35px;
    margin-bottom: 15px;
    font-size: 2em;
    font-weight: bold;
    position: relative;
    padding-left: 0;
}

.section-title::before {
    content: '';
}

.section-objective {
    font-style: italic;
    color: #6a737d;
    margin-top: -10px;
    margin-bottom: 20px;
}

.subsection-group {
    margin-bottom: 30px;
    border-left: 3px solid #e0e0e0;
    padding-left: 15px;
    margin-top: 25px;
}

.subsection-title {
    color: #4a4a4a;
    margin-top: 20px;
    margin-bottom: 10px;
    font-size: 1.6em;
    font-weight: 600;
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

.styled-list li strong {
    margin-right: 5px;
    color: #007bff;
}

.sub-styled-list {
    list-style: disc;
    margin-left: 25px;
    margin-top: 5px;
    margin-bottom: 5px;
}

.sub-styled-list li {
    margin-bottom: 5px;
    line-height: 1.4;
    color: #666;
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