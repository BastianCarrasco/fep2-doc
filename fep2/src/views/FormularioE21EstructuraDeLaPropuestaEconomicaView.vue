<script setup>
import { ref, onMounted } from 'vue';

const formData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/formulario-e21-estructura-de-la-propuesta-economica.json'); // Asegúrate que la ruta sea correcta
        formData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Formulario E-21:', error);
        errorMessage.value = 'No se pudo cargar la información del Formulario E-21.';
    }
});
</script>

<template>
    <div class="formulario-container">
        <h1 class="main-title" v-if="formData">{{ formData.titulo_formulario }}</h1>
        <h2 class="sub-title" v-if="formData">{{ formData.subtitulo }}</h2>

        <div v-if="formData" class="content">
            <div v-if="formData.instrucciones" class="instruction-section">
                <h3 class="subsection-title">{{ formData.instrucciones.titulo }}</h3>

                <!-- Consideraciones Críticas -->
                <div v-if="formData.instrucciones.consideraciones_criticas" class="sub-section-group">
                    <h4 class="sub-subsection-title">{{ formData.instrucciones.consideraciones_criticas.titulo }}</h4>
                    <p class="important-note">{{ formData.instrucciones.consideraciones_criticas.advertencia }}</p>
                    <p>{{ formData.instrucciones.consideraciones_criticas.entrega }}</p>
                </div>

                <!-- Estructura de Entregables -->
                <div v-if="formData.instrucciones.estructura_entregables" class="sub-section-group">
                    <h4 class="sub-subsection-title">{{ formData.instrucciones.estructura_entregables.titulo }}</h4>
                    <p>{{ formData.instrucciones.estructura_entregables.introduccion }}</p>

                    <div v-for="(entregable, eIndex) in formData.instrucciones.estructura_entregables.entregables"
                        :key="eIndex" class="entregable-block">
                        <h5 class="entregable-title">{{ entregable.titulo_entregable }}</h5>
                        <p class="entregable-description">{{ entregable.descripcion }}</p>

                        <div v-for="(sec, secIndex) in entregable.secciones" :key="secIndex" class="entregable-section">
                            <h6>{{ sec.numero }} {{ sec.titulo }}</h6>
                            <p v-if="sec.objetivo">{{ sec.objetivo }}</p>

                            <template v-if="sec.contenido_requerido">
                                <p v-if="sec.contenido_requerido.titulo" class="req-content-intro">{{
                                    sec.contenido_requerido.titulo }}</p>
                                <!-- Valores Totales (1.1) -->
                                <template v-if="sec.contenido_requerido.valores_totales">
                                    <p class="values-total-intro">{{ sec.contenido_requerido.valores_totales.titulo }}
                                    </p>
                                    <ul class="styled-list ordered-list">
                                        <li v-for="(punto, pIndex) in sec.contenido_requerido.valores_totales.puntos"
                                            :key="pIndex">{{ punto }}</li>
                                    </ul>
                                </template>
                                <!-- Otros puntos de contenido requerido -->
                                <ul v-if="sec.contenido_requerido.other_puntos || sec.contenido_requerido.puntos"
                                    class="styled-list">
                                    <li v-for="(punto, pIndex) in (sec.contenido_requerido.other_puntos || sec.contenido_requerido.puntos)"
                                        :key="pIndex">{{ punto }}</li>
                                </ul>

                                <!-- Hitos de Pago (1.2) -->
                                <template v-if="sec.contenido_requerido.hitos_pago">
                                    <p class="values-total-intro">{{ sec.contenido_requerido.hitos_pago.titulo }}</p>
                                    <ul class="styled-list">
                                        <li v-for="(punto, pIndex) in sec.contenido_requerido.hitos_pago.puntos"
                                            :key="pIndex">{{ punto }}</li>
                                    </ul>
                                </template>
                                <!-- Pagos Mensuales (1.2) -->
                                <template v-if="sec.contenido_requerido.pagos_mensuales">
                                    <p class="values-total-intro">{{ sec.contenido_requerido.pagos_mensuales.titulo }}
                                    </p>
                                    <ul class="styled-list">
                                        <li v-for="(punto, pIndex) in sec.contenido_requerido.pagos_mensuales.puntos"
                                            :key="pIndex">{{ punto }}</li>
                                    </ul>
                                </template>

                                <!-- Cuadro Maestro de Costos (2.1) -->
                                <template v-if="sec.contenido_requerido.cuadro_costos">
                                    <p class="values-total-intro">{{ sec.contenido_requerido.cuadro_costos.titulo }}</p>
                                    <ul class="styled-list">
                                        <li v-for="(punto, pIndex) in sec.contenido_requerido.cuadro_costos.puntos"
                                            :key="pIndex">{{ punto }}</li>
                                    </ul>
                                </template>
                                <!-- Cuadro Precio de Venta (2.1) -->
                                <template v-if="sec.contenido_requerido.cuadro_precio_venta">
                                    <p class="values-total-intro">{{ sec.contenido_requerido.cuadro_precio_venta.titulo
                                    }}</p>
                                    <ul class="styled-list">
                                        <li v-for="(punto, pIndex) in sec.contenido_requerido.cuadro_precio_venta.puntos"
                                            :key="pIndex">{{ punto }}</li>
                                    </ul>
                                </template>

                                <!-- VAN (2.2) -->
                                <template v-if="sec.contenido_requerido.van_tir">
                                    <p class="values-total-intro">{{ sec.contenido_requerido.van_tir.titulo }}</p>
                                    <ul class="styled-list sub-points">
                                        <li v-for="(punto, pIndex) in sec.contenido_requerido.van_tir.subpuntos"
                                            :key="pIndex">{{ punto }}</li>
                                    </ul>
                                </template>
                                <!-- TIR (2.2) -->
                                <template v-if="sec.contenido_requerido.tir">
                                    <p class="values-total-intro">{{ sec.contenido_requerido.tir.titulo }}</p>
                                    <ul class="styled-list sub-points">
                                        <li v-for="(punto, pIndex) in sec.contenido_requerido.tir.subpuntos"
                                            :key="pIndex">{{ punto }}</li>
                                    </ul>
                                </template>

                                <!-- Desglose de costos operacionales (2.5) -->
                                <template v-if="sec.contenido_requerido.desglose_costos">
                                    <p class="values-total-intro">{{ sec.contenido_requerido.desglose_costos.titulo }}
                                    </p>
                                    <ul class="styled-list">
                                        <li v-for="(punto, pIndex) in sec.contenido_requerido.desglose_costos.puntos"
                                            :key="pIndex">{{ punto }}</li>
                                    </ul>
                                    <p v-if="sec.contenido_requerido.optimizaciones" class="styled-list-item">{{
                                        sec.contenido_requerido.optimizaciones }}</p>
                                </template>

                                <!-- Excel de guía (3.1) -->
                                <template v-if="sec.contenido_requerido.excel_guia">
                                    <p class="values-total-intro">{{ sec.contenido_requerido.excel_guia.titulo }}</p>
                                    <ul class="styled-list">
                                        <li v-for="(punto, pIndex) in sec.contenido_requerido.excel_guia.puntos"
                                            :key="pIndex">{{ punto }}</li>
                                    </ul>
                                </template>
                                <!-- Obligatorio (3.2) -->
                                <template v-if="sec.obligatorio">
                                    <p class="values-total-intro">{{ sec.obligatorio.titulo }}</p>
                                    <ul class="styled-list">
                                        <li v-for="(punto, pIndex) in sec.obligatorio.puntos" :key="pIndex">{{ punto }}
                                        </li>
                                    </ul>
                                </template>
                            </template>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Requisitos Formales de Presentación -->
            <div v-if="formData.requisitos_formales_presentacion" class="instruction-section">
                <h3 class="subsection-title">{{ formData.requisitos_formales_presentacion.titulo }}</h3>
                <div v-if="formData.requisitos_formales_presentacion.formato_documentos" class="sub-section-group">
                    <h4 class="sub-subsection-title">{{
                        formData.requisitos_formales_presentacion.formato_documentos.titulo }}</h4>
                    <ul class="styled-list">
                        <li v-for="(punto, index) in formData.requisitos_formales_presentacion.formato_documentos.puntos"
                            :key="index">{{ punto }}</li>
                    </ul>
                </div>
                <div v-if="formData.requisitos_formales_presentacion.nomenclatura_archivos" class="sub-section-group">
                    <h4 class="sub-subsection-title">{{
                        formData.requisitos_formales_presentacion.nomenclatura_archivos.titulo }}
                    </h4>
                    <ul class="styled-list">
                        <li v-for="(punto, index) in formData.requisitos_formales_presentacion.nomenclatura_archivos.puntos"
                            :key="index">{{ punto }}</li>
                    </ul>
                </div>
                <div v-if="formData.requisitos_formales_presentacion.consistencia_obligatoria"
                    class="sub-section-group">
                    <h4 class="sub-subsection-title">{{
                        formData.requisitos_formales_presentacion.consistencia_obligatoria.titulo }}
                    </h4>
                    <ul class="styled-list">
                        <li v-for="(punto, index) in formData.requisitos_formales_presentacion.consistencia_obligatoria.puntos"
                            :key="index">{{ punto }}</li>
                    </ul>
                </div>
            </div>

            <!-- Notas Importantes -->
            <div v-if="formData.notas_importantes" class="instruction-section">
                <h3 class="subsection-title">{{ formData.notas_importantes.titulo }}</h3>
                <ul v-if="formData.notas_importantes.puntos" class="styled-list">
                    <li v-for="(punto, index) in formData.notas_importantes.puntos" :key="index"
                        :class="{ 'sub-styled-list-item': punto.startsWith('o ') }">{{ punto }}</li>
                </ul>
            </div>
            <p v-if="formData.recordatorio_final" class="important-note final-note">{{ formData.recordatorio_final }}
            </p>
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

.instruction-section {
    margin-top: 30px;
    margin-bottom: 30px;
    border-left: 4px solid #f0f0f0;
    padding-left: 20px;
}

.subsection-title {
    color: #4a4a4a;
    margin-top: 25px;
    margin-bottom: 15px;
    font-size: 1.6em;
    font-weight: bold;
    border-bottom: 1px dashed #eee;
    padding-bottom: 5px;
}

.sub-section-group {
    margin-top: 20px;
    margin-bottom: 20px;
    border-left: 2px solid #e9e9e9;
    padding-left: 15px;
}

.sub-subsection-title {
    color: #5d5d5d;
    margin-top: 18px;
    margin-bottom: 8px;
    font-size: 1.3em;
    font-weight: 500;
    border-bottom: 1px dotted #eee;
    padding-bottom: 5px;
}

.entregable-block {
    margin-top: 30px;
    margin-bottom: 30px;
    border: 1px solid #e0e0e0;
    border-radius: 5px;
    padding: 15px;
    background-color: #fcfdff;
}

.entregable-title {
    color: #0056b3;
    font-size: 1.4em;
    font-weight: bold;
    margin-bottom: 10px;
    border-bottom: 1px solid #d9edf7;
    padding-bottom: 8px;
}

.entregable-description {
    font-style: italic;
    color: #6a737d;
    margin-bottom: 15px;
}

.entregable-section h6 {
    color: #34495e;
    font-size: 1.1em;
    font-weight: bold;
    margin-top: 20px;
    margin-bottom: 10px;
}

.req-content-intro,
.values-total-intro {
    font-weight: bold;
    margin-top: 15px;
    margin-bottom: 5px;
    color: #333;
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
    list-style: decimal;
    /* Para listas como "1. Valor Total..." */
    margin-left: 20px;
    /* Ajusta la indentación para el número */
    padding-left: 0;
}

.styled-list.ordered-list li::before {
    content: '';
    /* Deshabilita el bullet personalizado */
}

.styled-list.sub-points {
    list-style: none;
    margin-left: 15px;
    padding-left: 10px;
}

.styled-list.sub-points li::before {
    content: 'o ';
    /* Para puntos como "o Identificación clara..." */
    position: static;
    color: #6a737d;
    /* Color más tenue para los 'o' */
    font-weight: normal;
    margin-right: 3px;
}

.styled-list-item {
    /* Para el punto de optimizaciones que no es parte de una lista con o */
    list-style: none;
    margin-left: 0;
    padding-left: 20px;
    position: relative;
}

.styled-list-item::before {
    content: '•';
    position: absolute;
    left: 0;
    color: #007bff;
    font-size: 1em;
    top: 0;
}


.important-note {
    font-weight: bold;
    color: #d9534f;
    margin-top: 20px;
    margin-bottom: 20px;
    padding: 10px 15px;
    border: 1px solid #d9534f;
    border-radius: 5px;
    background-color: #fdf7f7;
}

.final-note {
    font-size: 1.1em;
    text-align: center;
    margin-top: 40px;
    padding: 15px;
    background-color: #ffe0e0;
    border-color: #f0a0a0;
    color: #b30000;
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