<script setup>
import { ref, onMounted } from 'vue';

const capituloData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/bt-capitulo-9-requerimientos-tecnicos-funcionales-y-no-funcionales.json'); // Asegúrate que la ruta sea correcta
        capituloData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Capítulo 9 (Bases Técnicas):', error);
        errorMessage.value = 'No se pudo cargar la información del Capítulo 9 (Bases Técnicas).';
    }
});
</script>

<template>
    <div class="capitulo-container">
        <h1 class="main-title" v-if="capituloData">{{ capituloData.titulo_capitulo }}</h1>

        <div v-if="capituloData && capituloData.secciones_principales" class="content">
            <div v-for="seccion in capituloData.secciones_principales" :key="seccion.numero" class="section-block">
                <h2 class="section-title">{{ seccion.numero }} {{ seccion.titulo }}</h2>
                <p v-if="seccion.introduccion_arquitectura">{{ seccion.introduccion_arquitectura }}</p>

                <!-- Requisitos y Capas (9.1) -->
                <template v-if="seccion.requisitos_criticos">
                    <h3 class="subsection-title">{{ seccion.requisitos_criticos.titulo }}</h3>
                    <ul class="styled-list">
                        <li v-for="(punto, index) in seccion.requisitos_criticos.puntos" :key="index">{{ punto }}</li>
                    </ul>
                </template>
                <template v-if="seccion.capas_arquitectura">
                    <h3 class="subsection-title">{{ seccion.capas_arquitectura.titulo }}</h3>
                    <ul class="styled-list">
                        <li v-for="(punto, index) in seccion.capas_arquitectura.puntos" :key="index">{{ punto }}</li>
                    </ul>
                </template>

                <!-- Datacenter y Puestos BackOffice (9.2) -->
                <template v-if="seccion.datacenter_principal">
                    <h3 class="subsection-title">{{ seccion.datacenter_principal.titulo }}</h3>
                    <ul class="styled-list">
                        <li v-for="(punto, index) in seccion.datacenter_principal.puntos" :key="index">{{ punto }}</li>
                    </ul>
                </template>
                <template v-if="seccion.puestos_backoffice">
                    <h3 class="subsection-title">{{ seccion.puestos_backoffice.titulo }}</h3>
                    <ul class="styled-list">
                        <li v-for="(punto, index) in seccion.puestos_backoffice.puntos" :key="index">{{ punto }}</li>
                    </ul>
                </template>

                <!-- Puntos directos (9.3, 9.4) -->
                <ul v-if="seccion.puntos && !seccion.requisitos_criticos && !seccion.datacenter_principal && !seccion.obligatorias && !seccion.controles && !seccion.metricas_rendimiento && !seccion.estandares_ux_ui && !seccion.protocolos_estandares && !seccion.gestion_datos"
                    class="styled-list ordered-list">
                    <li v-for="(punto, index) in seccion.puntos" :key="index">{{ punto }}</li>
                </ul>

                <!-- Certificaciones Obligatorias y Personal (9.5) -->
                <template v-if="seccion.obligatorias">
                    <h3 class="subsection-title">{{ seccion.obligatorias.titulo }}</h3>
                    <ul class="styled-list">
                        <li v-for="(punto, index) in seccion.obligatorias.puntos" :key="index">{{ punto }}</li>
                    </ul>
                </template>
                <template v-if="seccion.personal">
                    <h3 class="subsection-title">{{ seccion.personal.titulo }}</h3>
                    <ul class="styled-list">
                        <li v-for="(punto, index) in seccion.personal.puntos" :key="index">{{ punto }}</li>
                    </ul>
                </template>

                <!-- Controles y Cumplimiento de Seguridad (9.6) -->
                <template v-if="seccion.controles">
                    <h3 class="subsection-title">{{ seccion.controles.titulo }}</h3>
                    <ul class="styled-list">
                        <li v-for="(punto, index) in seccion.controles.puntos" :key="index">{{ punto }}</li>
                    </ul>
                </template>
                <template v-if="seccion.cumplimiento">
                    <h3 class="subsection-title">{{ seccion.cumplimiento.titulo }}</h3>
                    <ul class="styled-list">
                        <li v-for="(punto, index) in seccion.cumplimiento.puntos" :key="index">{{ punto }}</li>
                    </ul>
                </template>

                <!-- Métricas de Rendimiento (9.7) -->
                <template v-if="seccion.metricas_rendimiento">
                    <h3 class="subsection-title">{{ seccion.metricas_rendimiento.titulo }}</h3>
                    <ul class="styled-list">
                        <li v-for="(punto, index) in seccion.metricas_rendimiento.puntos" :key="index">{{ punto }}</li>
                    </ul>
                </template>

                <!-- Estándares UX/UI (9.8) -->
                <template v-if="seccion.estandares_ux_ui">
                    <h3 class="subsection-title">{{ seccion.estandares_ux_ui.titulo }}</h3>
                    <ul class="styled-list">
                        <li v-for="(punto, index) in seccion.estandares_ux_ui.puntos" :key="index">{{ punto }}</li>
                    </ul>
                </template>

                <!-- Protocolos y Estándares de Integración (9.9) -->
                <template v-if="seccion.protocolos_estandares">
                    <h3 class="subsection-title">{{ seccion.protocolos_estandares.titulo }}</h3>
                    <ul class="styled-list">
                        <li v-for="(punto, index) in seccion.protocolos_estandares.puntos" :key="index">{{ punto }}</li>
                    </ul>
                </template>

                <!-- Gestión de Datos (9.10) -->
                <template v-if="seccion.gestion_datos">
                    <h3 class="subsection-title">{{ seccion.gestion_datos.titulo }}</h3>
                    <ul class="styled-list">
                        <li v-for="(punto, index) in seccion.gestion_datos.puntos" :key="index">{{ punto }}</li>
                    </ul>
                </template>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Capítulo 9: Requerimientos Técnicos, Funcionales y No Funcionales
            (Bases
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

.styled-list.ordered-list li {
    padding-left: 0;
}

.styled-list.ordered-list li::before {
    content: '';
    position: static;
    margin-right: 5px;
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