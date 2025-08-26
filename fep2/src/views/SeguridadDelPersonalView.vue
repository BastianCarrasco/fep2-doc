<script setup>
import { ref, onMounted } from 'vue';

const seguridadPersonalData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textos/seguridad-del-personal.json'); // Ajusta la ruta a tu archivo JSON
        seguridadPersonalData.value = response.default;
    } catch (error) {
        console.error('Error al cargar la sección "Seguridad del personal":', error);
        errorMessage.value = 'No se pudo cargar la información de "Seguridad del personal".';
    }
});
</script>

<template>
    <div class="seguridad-personal-container">
        <h1 class="main-title" v-if="seguridadPersonalData">{{ seguridadPersonalData.titulo_seccion }}</h1>

        <div v-if="seguridadPersonalData && seguridadPersonalData.secciones" class="content">
            <div v-for="section in seguridadPersonalData.secciones" :key="section.numero" class="section-group">
                <h2 class="section-title">{{ section.numero }} {{ section.titulo }}</h2>
                <p v-if="section.objetivo" class="section-objective">Objetivo: {{ section.objetivo }}</p>
                <p v-if="section.parrafo_introductorio">{{ section.parrafo_introductorio }}</p>
                <p v-if="section.introduccion && section.numero === '6.2'">{{ section.introduccion }}</p>
                <p v-if="section.introduccion && section.numero === '6.3'">{{ section.introduccion }}</p>

                <div v-for="subsection in section.subsecciones" :key="subsection.numero" class="subsection-group">
                    <h3 class="subsection-title">{{ subsection.numero }} {{ subsection.titulo }}</h3>
                    <p
                        v-if="subsection.contenido && (subsection.numero === '6.1.1' || subsection.numero === '6.2.1' || subsection.numero === '6.3.2' || subsection.numero === '6.3.4' || subsection.numero === '6.3.5')">
                        {{ subsection.contenido }}</p>
                    <p v-if="subsection.verificaciones_contratacion">{{ subsection.verificaciones_contratacion }}</p>
                    <ul v-if="subsection.controles_verificacion" class="styled-list">
                        <li v-for="(control, index) in subsection.controles_verificacion" :key="index">
                            <strong>{{ control.letra }}</strong> {{ control.item }}
                        </li>
                    </ul>
                    <p v-if="subsection.revision_antecedentes_financieros">{{
                        subsection.revision_antecedentes_financieros }}</p>
                    <p v-if="subsection.personal_temporal_externo">{{ subsection.personal_temporal_externo }}</p>
                    <p v-if="subsection.supervision_personal_nuevo">{{ subsection.supervision_personal_nuevo }}</p>
                    <p v-if="subsection.circunstancias_personales">{{ subsection.circunstancias_personales }}</p>

                    <p
                        v-if="subsection.introduccion && (subsection.numero === '6.1.3' || subsection.numero === '6.3.3')">
                        {{ subsection.introduccion }}</p>
                    <p v-if="subsection.personal_temporal_terceros">{{ subsection.personal_temporal_terceros }}</p>
                    <p v-if="subsection.revision_acuerdos">{{ subsection.revision_acuerdos }}</p>

                    <p v-if="subsection.responsabilidad_seguridad">{{ subsection.responsabilidad_seguridad }}</p>
                    <p v-if="subsection.derechos_legales">{{ subsection.derechos_legales }}</p>

                    <p v-if="subsection.contenido_general && subsection.numero === '6.3.1'">{{
                        subsection.contenido_general }}</p>
                    <p v-if="subsection.procedimiento_formal && subsection.numero === '6.3.1'">{{
                        subsection.procedimiento_formal }}</p>

                    <p v-if="subsection.acciones_considerar">{{ subsection.acciones_considerar }}</p>
                    <ul v-if="subsection.acciones_considerar" class="styled-list">
                        <li v-for="(accion, index) in subsection.acciones_considerar" :key="index">
                            <strong>{{ accion.letra }}</strong> {{ accion.item }}
                        </li>
                    </ul>
                    <p v-if="subsection.recuperacion_software">{{ subsection.recuperacion_software }}</p>

                </div>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Seguridad del personal"...</p>
    </div>
</template>

<style scoped>
/* Copia y pega los estilos generales de tus otras vistas aquí. */
/* Renombra la clase principal del contenedor si la cambiaste en el template. */
.seguridad-personal-container {
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
    /* Si tienes sub-sublistas con discos */
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