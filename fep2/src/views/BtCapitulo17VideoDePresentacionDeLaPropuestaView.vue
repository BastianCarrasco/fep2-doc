<script setup>
import { ref, onMounted } from 'vue';

const capituloData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/bt-capitulo-17-video-de-presentacion-de-la-propuesta.json'); // Asegúrate que la ruta sea correcta
        capituloData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Capítulo 17 (Bases Técnicas):', error);
        errorMessage.value = 'No se pudo cargar la información del Capítulo 17 (Bases Técnicas).';
    }
});
</script>

<template>
    <div class="capitulo-container">
        <h1 class="main-title" v-if="capituloData">{{ capituloData.titulo_capitulo }}</h1>

        <div v-if="capituloData && capituloData.secciones_principales" class="content">
            <div v-for="seccion in capituloData.secciones_principales" :key="seccion.numero" class="section-block">
                <h2 class="section-title">{{ seccion.numero }} {{ seccion.titulo }}</h2>

                <div v-for="subsection in seccion.subsecciones" :key="subsection.numero" class="sub-section-group">
                    <h3 class="subsection-title">{{ subsection.numero }} {{ subsection.titulo }}</h3>
                    <p v-if="subsection.introduccion">{{ subsection.introduccion }}</p>

                    <!-- 17.1.1 Requisitos Técnicos Obligatorios -->
                    <template v-if="subsection.numero === '17.1.1'">
                        <div v-if="subsection.formato_y_calidad">
                            <h4 class="sub-subsection-title">{{ subsection.formato_y_calidad.titulo }}</h4>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.formato_y_calidad.puntos" :key="index">{{ punto
                                    }}</li>
                            </ul>
                        </div>
                        <div v-if="subsection.audio">
                            <h4 class="sub-subsection-title">{{ subsection.audio.titulo }}</h4>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.audio.puntos" :key="index">{{ punto }}</li>
                            </ul>
                        </div>
                        <div v-if="subsection.aspectos_visuales">
                            <h4 class="sub-subsection-title">{{ subsection.aspectos_visuales.titulo }}</h4>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.aspectos_visuales.puntos" :key="index">{{ punto
                                    }}</li>
                            </ul>
                        </div>
                    </template>

                    <!-- 17.1.2 Estructura y Contenido Obligatorio -->
                    <template v-if="subsection.numero === '17.1.2'">
                        <div v-for="segmento in subsection.segmentos" :key="segmento.numero" class="segment-block">
                            <h4 class="sub-subsection-title">{{ segmento.numero }}. {{ segmento.titulo }}</h4>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in segmento.puntos" :key="index">{{ punto }}</li>
                            </ul>
                        </div>
                    </template>

                    <!-- 17.2.1 Requisitos de Aparición -->
                    <template v-if="subsection.numero === '17.2.1'">
                        <p v-if="subsection.obligatorio">{{ subsection.obligatorio }}</p>
                        <p v-if="subsection.integrante_individual">{{ subsection.integrante_individual }}</p>
                        <ul v-if="subsection.puntos_integrante" class="styled-list">
                            <li v-for="(punto, index) in subsection.puntos_integrante" :key="index">{{ punto }}</li>
                        </ul>
                        <p v-if="subsection.identificacion_en_pantalla">{{ subsection.identificacion_en_pantalla }}</p>
                        <ul v-if="subsection.puntos_identificacion" class="styled-list">
                            <li v-for="(punto, index) in subsection.puntos_identificacion" :key="index">{{ punto }}</li>
                        </ul>
                    </template>

                    <!-- 17.3.1 Causales de Penalización o Descalificación -->
                    <template v-if="subsection.numero === '17.3.1'">
                        <div v-if="subsection.penalizaciones">
                            <h4 class="sub-subsection-title">{{ subsection.penalizaciones.titulo }}</h4>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.penalizaciones.puntos" :key="index">{{ punto }}
                                </li>
                            </ul>
                        </div>
                        <div v-if="subsection.descalificacion_automatica">
                            <h4 class="sub-subsection-title">{{ subsection.descalificacion_automatica.titulo }}</h4>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.descalificacion_automatica.puntos" :key="index">
                                    {{ punto }}</li>
                            </ul>
                        </div>
                    </template>

                    <!-- 17.4.1 Requisitos de Uniformidad -->
                    <template v-if="subsection.numero === '17.4.1'">
                        <div v-if="subsection.aspectos_visuales">
                            <h4 class="sub-subsection-title">{{ subsection.aspectos_visuales.titulo }}</h4>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.aspectos_visuales.puntos" :key="index">{{ punto
                                    }}</li>
                            </ul>
                        </div>
                        <div v-if="subsection.aspectos_audio">
                            <h4 class="sub-subsection-title">{{ subsection.aspectos_audio.titulo }}</h4>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.aspectos_audio.puntos" :key="index">{{ punto }}
                                </li>
                            </ul>
                        </div>
                        <div v-if="subsection.identidad_corporativa">
                            <h4 class="sub-subsection-title">{{ subsection.identidad_corporativa.titulo }}</h4>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.identidad_corporativa.puntos" :key="index">{{
                                    punto }}</li>
                            </ul>
                        </div>
                    </template>

                    <!-- 17.5.1 Medios de Entrega -->
                    <template v-if="subsection.numero === '17.5.1'">
                        <div v-for="(opcion, index) in subsection.opciones_entrega" :key="index" class="option-block">
                            <h4 class="sub-subsection-title">{{ opcion.titulo }}</h4>
                            <ul class="styled-list">
                                <li v-for="(punto, pIndex) in opcion.puntos" :key="pIndex">{{ punto }}</li>
                            </ul>
                        </div>
                    </template>

                    <!-- 17.6.1 Cesión de Derechos -->
                    <template v-if="subsection.numero === '17.6.1'">
                        <ul v-if="subsection.puntos" class="styled-list">
                            <li v-for="(punto, index) in subsection.puntos" :key="index">{{ punto }}</li>
                        </ul>
                    </template>

                    <!-- 17.6.2 Protección de Información -->
                    <template v-if="subsection.numero === '17.6.2'">
                        <ul v-if="subsection.puntos" class="styled-list">
                            <li v-for="(punto, index) in subsection.puntos" :key="index">{{ punto }}</li>
                        </ul>
                    </template>
                </div>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Capítulo 17: Video de Presentación de la Propuesta (Bases
            Técnicas)"...</p>
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

.section-block {
    margin-bottom: 45px;
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

.sub-section-group {
    margin-top: 25px;
    margin-bottom: 25px;
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

.sub-subsection-title {
    color: #5d5d5d;
    margin-top: 18px;
    margin-bottom: 8px;
    font-size: 1.3em;
    font-weight: 500;
    border-bottom: 1px dashed #eee;
    padding-bottom: 5px;
}

.segment-block,
.option-block {
    margin-top: 15px;
    margin-left: 10px;
    border-left: 1px solid #f0f0f0;
    padding-left: 10px;
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