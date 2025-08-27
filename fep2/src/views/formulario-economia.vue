<script setup>
import { ref, onMounted } from 'vue';

const formData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/formulario-economia.json'); // Asegúrate que la ruta sea correcta
        formData.value = response.default['Formulario-E21-Estructura-De-La-Propuesta-Economica']; // Acceder al objeto principal
    } catch (error) {
        console.error('Error al cargar el Formulario E-21:', error);
        errorMessage.value = 'No se pudo cargar la información del Formulario E-21.';
    }
});

// Función auxiliar para renderizar listas o párrafos
const renderContent = (content) => {
    if (Array.isArray(content)) {
        return content.map((item, index) => {
            if (typeof item === 'string') {
                if (item.startsWith('o ')) {
                    return `<li key="${index}" class="list-item-sub">${item.substring(2)}</li>`;
                }
                return `<li key="${index}" class="list-item">${item}</li>`;
            }
            // Si el contenido es un objeto (ej. para secciones más complejas), puedes manejarlo aquí
            return `<p key="${index}" class="content-paragraph">${item}</p>`;
        }).join('');
    }
    return `<p class="content-paragraph">${content}</p>`;
};
</script>

<template>
    <div class="formulario-container">
        <h1 class="main-title" v-if="formData">{{ formData.titulo_formulario }}</h1>
        <h2 class="sub-title" v-if="formData">{{ formData.subtitulo }}</h2>

        <div v-if="formData" class="content">
            <div class="section-block">
                <h3 class="subsection-title">{{ formData.instrucciones_oferta_economica.titulo }}</h3>

                <!-- CONSIDERACIONES CRÍTICAS -->
                <div class="sub-section-item">
                    <p class="field-header">{{ formData.instrucciones_oferta_economica.consideraciones_criticas.titulo
                        }}</p>
                    <p class="text-warning">{{
                        formData.instrucciones_oferta_economica.consideraciones_criticas.advertencia }}</p>
                    <p class="text-normal">{{
                        formData.instrucciones_oferta_economica.consideraciones_criticas.entrega_separada }}</p>
                </div>

                <!-- ESTRUCTURA DE ENTREGABLES -->
                <div class="sub-section-item">
                    <p class="field-header">{{ formData.instrucciones_oferta_economica.estructura_entregables.titulo }}
                    </p>
                    <p class="text-normal">{{ formData.instrucciones_oferta_economica.estructura_entregables.descripcion
                        }}</p>

                    <!-- ENTREGABLE 1 -->
                    <div class="entregable-block">
                        <h4 class="entregable-title">{{
                            formData.instrucciones_oferta_economica.estructura_entregables.entregable_1.titulo }}</h4>
                        <p class="entregable-description">{{
                            formData.instrucciones_oferta_economica.estructura_entregables.entregable_1.descripcion }}
                        </p>
                        <div v-for="(seccionEnt1, indexEnt1) in formData.instrucciones_oferta_economica.estructura_entregables.entregable_1.secciones"
                            :key="indexEnt1" class="entregable-section-item">
                            <p class="sub-section-header">{{ seccionEnt1.titulo }}</p>
                            <p class="sub-section-objective">Objetivo: {{ seccionEnt1.objetivo }}</p>
                            <div v-if="seccionEnt1.contenido_requerido">
                                <p class="sub-section-content-title">Contenido Requerido:</p>
                                <ul class="content-list" v-html="renderContent(seccionEnt1.contenido_requerido)"></ul>
                            </div>
                        </div>
                    </div>

                    <!-- ENTREGABLE 2 -->
                    <div class="entregable-block">
                        <h4 class="entregable-title">{{
                            formData.instrucciones_oferta_economica.estructura_entregables.entregable_2.titulo }}</h4>
                        <p class="entregable-description">{{
                            formData.instrucciones_oferta_economica.structure_entregables.entregable_2.descripcion }}
                        </p>
                        <div v-for="(seccionEnt2, indexEnt2) in formData.instrucciones_oferta_economica.estructura_entregables.entregable_2.secciones"
                            :key="indexEnt2" class="entregable-section-item">
                            <p class="sub-section-header">{{ seccionEnt2.titulo }}</p>
                            <p class="sub-section-objective">Objetivo: {{ seccionEnt2.objetivo }}</p>
                            <div v-if="seccionEnt2.contenido_requerido">
                                <p class="sub-section-content-title">Contenido Requerido:</p>
                                <ul class="content-list" v-html="renderContent(seccionEnt2.contenido_requerido)"></ul>
                            </div>
                        </div>
                    </div>

                    <!-- ENTREGABLE 3 -->
                    <div class="entregable-block">
                        <h4 class="entregable-title">{{
                            formData.instrucciones_oferta_economica.estructura_entregables.entregable_3.titulo }}</h4>
                        <p class="entregable-description">{{
                            formData.instrucciones_oferta_economica.estructura_entregables.entregable_3.descripcion }}
                        </p>
                        <div v-for="(seccionEnt3, indexEnt3) in formData.instrucciones_oferta_economica.estructura_entregables.entregable_3.secciones"
                            :key="indexEnt3" class="entregable-section-item">
                            <p class="sub-section-header">{{ seccionEnt3.titulo }}</p>
                            <p class="sub-section-objective" v-if="seccionEnt3.objetivo">Objetivo: {{
                                seccionEnt3.objetivo }}</p>
                            <div v-if="seccionEnt3.contenido_requerido">
                                <p class="sub-section-content-title">Contenido Requerido:</p>
                                <ul class="content-list" v-html="renderContent(seccionEnt3.contenido_requerido)"></ul>
                            </div>
                            <div v-if="seccionEnt3.obligatorio">
                                <p class="sub-section-content-title">Obligatorio:</p>
                                <ul class="content-list" v-html="renderContent(seccionEnt3.obligatorio)"></ul>
                            </div>
                            <div v-if="seccionEnt3.se_evaluara">
                                <p class="sub-section-content-title">Se evaluará:</p>
                                <ul class="content-list" v-html="renderContent(seccionEnt3.se_evaluara)"></ul>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- REQUISITOS FORMALES DE PRESENTACIÓN -->
                <div class="sub-section-item">
                    <p class="field-header">{{
                        formData.instrucciones_oferta_economica.requisitos_formales_presentacion.titulo }}</p>
                    <div
                        v-if="formData.instrucciones_oferta_economica.requisitos_formales_presentacion.formato_documentos">
                        <p class="sub-section-content-title">Formato de Documentos:</p>
                        <ul class="content-list"
                            v-html="renderContent(formData.instrucciones_oferta_economica.requisitos_formales_presentacion.formato_documentos)">
                        </ul>
                    </div>
                </div>

            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Formulario E-21"...</p>
    </div>
</template>

<style scoped>
.formulario-container {
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
    margin-bottom: 5px;
    font-size: 2em;
    font-weight: bold;
    text-align: center;
}

.sub-title {
    color: #007bff;
    margin-bottom: 30px;
    border-bottom: 2px solid #007bff;
    padding-bottom: 10px;
    font-size: 1.5em;
    font-weight: 600;
    text-align: center;
}

.section-block {
    margin-bottom: 30px;
    border-left: 3px solid #e0e0e0;
    padding-left: 15px;
}

.subsection-title {
    color: #4a4a4a;
    margin-top: 20px;
    margin-bottom: 15px;
    font-size: 1.4em;
    font-weight: bold;
}

.sub-section-item {
    margin-bottom: 25px;
    padding-left: 10px;
    border-left: 2px solid #f0f0f0;
}

.field-header {
    font-weight: bold;
    font-size: 1.2em;
    margin-bottom: 10px;
    color: #222;
}

.text-warning {
    color: #d32f2f;
    font-weight: bold;
    margin-bottom: 10px;
    line-height: 1.5;
}

.text-normal {
    color: #444;
    margin-bottom: 10px;
}

.entregable-block {
    margin-top: 25px;
    margin-bottom: 30px;
    padding: 15px;
    background-color: #f9f9f9;
    border: 1px solid #e0e0e0;
    border-radius: 5px;
}

.entregable-title {
    color: #007bff;
    font-size: 1.3em;
    font-weight: bold;
    margin-bottom: 10px;
    border-bottom: 1px dashed #cce0ff;
    padding-bottom: 5px;
}

.entregable-description {
    font-style: italic;
    color: #666;
    margin-bottom: 15px;
}

.entregable-section-item {
    margin-top: 20px;
    margin-bottom: 20px;
    padding-left: 10px;
}

.sub-section-header {
    font-weight: bold;
    color: #333;
    font-size: 1.1em;
    margin-bottom: 8px;
}

.sub-section-objective {
    font-style: italic;
    color: #555;
    margin-bottom: 10px;
}

.sub-section-content-title {
    font-weight: 600;
    color: #444;
    margin-top: 10px;
    margin-bottom: 5px;
}

.content-list {
    list-style-type: disc;
    margin-left: 25px;
    padding: 0;
}

.list-item {
    margin-bottom: 5px;
    color: #444;
}

.list-item-sub {
    list-style-type: circle;
    margin-left: 20px;
    margin-bottom: 3px;
    color: #666;
}

.content-paragraph {
    margin-bottom: 5px;
    color: #444;
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