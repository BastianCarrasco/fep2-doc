<script setup>
import { ref, onMounted } from 'vue';

const introData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        // Importa el JSON de la introducción. Asegúrate que la ruta sea correcta.
        const response = await import('../textos/intro.json');
        introData.value = response.default; // Accede al contenido por .default
    } catch (error) {
        console.error('Error al cargar la introducción:', error);
        errorMessage.value = 'No se pudo cargar la información de la introducción.';
    }
});

// Función auxiliar para renderizar listas de puntos si es necesario
const renderPoints = (points) => {
    if (!points || points.length === 0) return null;
    return points.map(p => {
        let text = p.item || p.definicion; // Usa 'item' o 'definicion'
        if (p.letra) {
            text = p.letra + ' ' + text;
        }
        return text;
    }).filter(Boolean);
};
</script>

<template>
    <div class="intro-container">
        <h1 class="main-title" v-if="introData">{{ introData.titulo_seccion }}</h1>

        <div v-if="introData" class="intro-content">
            <!-- Sección: ¿Qué es la seguridad de la información? -->
            <div class="section-block">
                <h2 class="section-title">¿Qué es la seguridad de la información?</h2>
                <p>{{ introData.que_es_seguridad_informacion.introduccion }}</p>
                <p>{{ introData.que_es_seguridad_informacion.formas_informacion }}</p>

                <h3 class="subsection-title">La seguridad de la información se caracteriza aquí como la preservación de
                    la:</h3>
                <ul class="styled-list">
                    <li v-for="(char, index) in introData.que_es_seguridad_informacion.caracteristicas_seguridad.puntos"
                        :key="index">
                        <strong>{{ char.concepto }}:</strong> {{ char.definicion }}
                    </li>
                </ul>
                <p>{{ introData.que_es_seguridad_informacion.implementacion }}</p>
            </div>

            <!-- Sección: ¿Por qué es necesaria la seguridad de la información? -->
            <div class="section-block">
                <h2 class="section-title">¿Por qué es necesaria la seguridad de la información?</h2>
                <p>{{ introData.por_que_es_necesaria_seguridad_informacion.importancia_activos }}</p>
                <p>{{ introData.por_que_es_necesaria_seguridad_informacion.amenazas_crecientes }}</p>
                <p>{{ introData.por_que_es_necesaria_seguridad_informacion.vulnerabilidad }}</p>
                <p>{{ introData.por_que_es_necesaria_seguridad_informacion.limitaciones_tecnicas }}</p>
                <p>{{ introData.por_que_es_necesaria_seguridad_informacion.participacion_necesaria }}</p>
                <p>{{ introData.por_que_es_necesaria_seguridad_informacion.costo_beneficio_diseño }}</p>
            </div>

            <!-- Sección: ¿Cómo establecer los requisitos de seguridad? -->
            <div class="section-block">
                <h2 class="section-title">¿Cómo establecer los requisitos de seguridad?</h2>
                <p>{{ introData.como_establecer_requisitos_seguridad.esencial }}</p>
                <ul class="styled-list">
                    <li v-for="(fuente, index) in introData.como_establecer_requisitos_seguridad.fuentes_principales"
                        :key="index">
                        <strong>{{ fuente.orden }}:</strong> {{ fuente.descripcion }}
                    </li>
                </ul>
            </div>

            <!-- Sección: Evaluación de los riesgos de la seguridad -->
            <div class="section-block">
                <h2 class="section-title">Evaluación de los riesgos de la seguridad</h2>
                <p>{{ introData.evaluacion_riesgos_seguridad.metodo_identificacion }}</p>
                <p>{{ introData.evaluacion_riesgos_seguridad.aplicacion }}</p>
                <h3 class="subsection-title">{{
                    introData.evaluacion_riesgos_seguridad.consideracion_sistematica.descripcion }}</h3>
                <ul class="styled-list">
                    <li v-for="(punto, index) in introData.evaluacion_riesgos_seguridad.consideracion_sistematica.puntos"
                        :key="index">
                        {{ punto.letra }} {{ punto.item }}
                    </li>
                </ul>
                <p>{{ introData.evaluacion_riesgos_seguridad.resultados_guia }}</p>
                <h3 class="subsection-title">{{ introData.evaluacion_riesgos_seguridad.revisiones_periodicas.descripcion
                    }}</h3>
                <ul class="styled-list">
                    <li v-for="(punto, index) in introData.evaluacion_riesgos_seguridad.revisiones_periodicas.puntos"
                        :key="index">
                        {{ punto.letra }} {{ punto.item }}
                    </li>
                </ul>
                <p>{{ introData.evaluacion_riesgos_seguridad.niveles_profundidad_revision }}</p>
            </div>

            <!-- Sección: Selección de controles -->
            <div class="section-block">
                <h2 class="section-title">Selección de controles</h2>
                <p>{{ introData.seleccion_controles.criterios }}</p>
                <p>{{ introData.seleccion_controles.fuentes_controles }}</p>
                <p>{{ introData.seleccion_controles.bases_seleccion }}</p>
                <p>{{ introData.seleccion_controles.principios_guias }}</p>
            </div>

            <!-- Sección: Punto de partida de la seguridad de la información -->
            <div class="section-block">
                <h2 class="section-title">Punto de partida de la seguridad de la información</h2>
                <p>{{ introData.punto_partida_seguridad_informacion.descripcion }}</p>
                <h3 class="subsection-title">{{
                    introData.punto_partida_seguridad_informacion.controles_esenciales_legislativos.descripcion }}</h3>
                <ul class="styled-list">
                    <li v-for="(punto, index) in introData.punto_partida_seguridad_informacion.controles_esenciales_legislativos.puntos"
                        :key="index">
                        {{ punto.letra }} {{ punto.item }}
                    </li>
                </ul>
                <h3 class="subsection-title">{{
                    introData.punto_partida_seguridad_informacion.controles_mejor_practica.descripcion }}</h3>
                <ul class="styled-list">
                    <li v-for="(punto, index) in introData.punto_partida_seguridad_informacion.controles_mejor_practica.puntos"
                        :key="index">
                        {{ punto.letra }} {{ punto.item }}
                    </li>
                </ul>
                <p>{{ introData.punto_partida_seguridad_informacion.consideracion_final }}</p>
            </div>

            <!-- Sección: Factores críticos para el éxito -->
            <div class="section-block">
                <h2 class="section-title">Factores críticos para el éxito</h2>
                <p>{{ introData.factores_criticos_exito.descripcion }}</p>
                <ul class="styled-list">
                    <li v-for="(factor, index) in introData.factores_criticos_exito.puntos" :key="index">
                        {{ factor.letra }} {{ factor.item }}
                    </li>
                </ul>
            </div>

            <!-- Sección: Desarrollo de guías propias -->
            <div class="section-block">
                <h2 class="section-title">Desarrollo de guías propias</h2>
                <p>{{ introData.desarrollo_guias_propias.consideracion_codigo }}</p>
                <p>{{ introData.desarrollo_guias_propias.referencias_cruzadas }}</p>
            </div>

        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando introducción...</p>
    </div>
</template>

<style scoped>
/* Puedes copiar y pegar la mayoría de los estilos de PreambuloView.vue aquí */
/* O si quieres, puedes crear un archivo de estilos compartido para las vistas */
.intro-container {
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