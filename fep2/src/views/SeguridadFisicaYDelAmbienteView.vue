<script setup>
import { ref, onMounted } from 'vue';

const seguridadFisicaData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textos/seguridad-fisica-y-del-ambiente.json'); // Ajusta la ruta
        seguridadFisicaData.value = response.default;
    } catch (error) {
        console.error('Error al cargar la sección "Seguridad física y del ambiente":', error);
        errorMessage.value = 'No se pudo cargar la información de "Seguridad física y del ambiente".';
    }
});
</script>

<template>
    <div class="seguridad-fisica-container">
        <h1 class="main-title" v-if="seguridadFisicaData">{{ seguridadFisicaData.titulo_seccion }}</h1>

        <div v-if="seguridadFisicaData && seguridadFisicaData.secciones" class="content">
            <div v-for="section in seguridadFisicaData.secciones" :key="section.numero" class="section-group">
                <h2 class="section-title">{{ section.numero }} {{ section.titulo }}</h2>
                <p v-if="section.objetivo" class="section-objective">Objetivo: {{ section.objetivo }}</p>
                <p v-if="section.introduccion && section.numero === '7.2'">{{ section.introduccion }}</p>
                <p v-if="section.introduccion && section.numero === '7.3'">{{ section.introduccion }}</p>
                <p v-if="section.referencia_adicional">{{ section.referencia_adicional }}</p>


                <div v-for="subsection in section.subsecciones" :key="subsection.numero" class="subsection-group">
                    <h3 class="subsection-title">{{ subsection.numero }} {{ subsection.titulo }}</h3>
                    <p v-if="subsection.parrafo_introductorio">{{ subsection.parrafo_introductorio }}</p>
                    <p
                        v-if="subsection.introduccion && subsection.numero !== '7.2.1' && subsection.numero !== '7.3.1' && subsection.numero !== '7.3.2'">
                        {{ subsection.introduccion }}</p>
                    <p v-if="subsection.introduccion && subsection.numero === '7.2.1'">{{ subsection.introduccion }}</p>
                    <p v-if="subsection.introduccion && subsection.numero === '7.3.1'">{{ subsection.introduccion }}</p>
                    <p v-if="subsection.introduccion && subsection.numero === '7.3.2'">{{ subsection.introduccion }}</p>


                    <p
                        v-if="subsection.controles_considerar && ['7.1.3', '7.1.4', '7.1.5', '7.2.1', '7.2.3', '7.2.4', '7.3.1'].includes(subsection.numero)">
                        {{ subsection.controles_considerar }}</p>
                    <ul v-if="subsection.puntos_controles" class="styled-list">
                        <li v-for="(control, index) in subsection.puntos_controles" :key="index">
                            <strong>{{ control.letra }}</strong> {{ control.item }}
                            <ul v-if="control.subpuntos" class="sub-styled-list">
                                <li v-for="(subpunto, subIndex) in control.subpuntos" :key="subIndex">
                                    {{ subpunto }}
                                </li>
                            </ul>
                        </li>
                    </ul>

                    <p v-if="subsection.opciones_continuidad">{{ subsection.opciones_continuidad }}</p>
                    <ul v-if="subsection.puntos_opciones" class="styled-list">
                        <li v-for="(opcion, index) in subsection.puntos_opciones" :key="index">
                            <strong>{{ opcion.letra }}</strong> {{ opcion.item }}
                        </li>
                    </ul>
                    <p v-if="subsection.recomendacion_ups">{{ subsection.recomendacion_ups }}</p>
                    <p v-if="subsection.generador_respaldo">{{ subsection.generador_respaldo }}</p>
                    <p v-if="subsection.adicionales">{{ subsection.adicionales }}</p>

                    <p v-if="subsection.guias_considerar">{{ subsection.guias_considerar }}</p>
                    <ul v-if="subsection.puntos_guias" class="styled-list">
                        <li v-for="(guia, index) in subsection.puntos_guias" :key="index">
                            <strong>{{ guia.letra }}</strong> {{ guia.item }}
                        </li>
                    </ul>
                    <p v-if="subsection.riesgos_seguridad_variados">{{ subsection.riesgos_seguridad_variados }}</p>

                    <p v-if="subsection.revision_dispositivos">{{ subsection.revision_dispositivos }}</p>

                    <p v-if="subsection.daño_desastre">{{ subsection.daño_desastre }}</p>

                </div>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Seguridad física y del ambiente"...</p>
    </div>
</template>

<style scoped>
/* Copia y pega los estilos generales de tus otras vistas aquí. */
.seguridad-fisica-container {
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
    /* Para sub-listas dentro de los puntos (ej. d.1, d.2) */
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