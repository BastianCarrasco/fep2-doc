<script setup>
import { ref, onMounted } from 'vue';

const controlAccesoData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textos/control-de-acceso.json'); // Ajusta la ruta
        controlAccesoData.value = response.default;
    } catch (error) {
        console.error('Error al cargar la sección "Control de acceso":', error);
        errorMessage.value = 'No se pudo cargar la información de "Control de acceso".';
    }
});
</script>

<template>
    <div class="control-acceso-container">
        <h1 class="main-title" v-if="controlAccesoData">{{ controlAccesoData.titulo_seccion }}</h1>

        <div v-if="controlAccesoData && controlAccesoData.secciones" class="content">
            <div v-for="section in controlAccesoData.secciones" :key="section.numero" class="section-group">
                <h2 class="section-title">{{ section.numero }} {{ section.titulo }}</h2>
                <p v-if="section.objetivo" class="section-objective">Objetivo: {{ section.objetivo }}</p>
                <p v-if="section.introduccion && section.numero === '9.1'">{{ section.introduccion }}</p>
                <p v-if="section.descripcion && section.numero === '9.1'">{{ section.descripcion }}</p>
                <ul v-if="section.consideraciones && section.numero === '9.1'" class="styled-list">
                    <li v-for="(consideracion, index) in section.consideraciones" :key="index">
                        <strong>{{ consideracion.letra }}</strong> {{ consideracion.item }}
                    </li>
                </ul>

                <!-- Subsecciones (9.2, 9.3, 9.4, 9.5, 9.6, 9.7, 9.8) -->
                <div v-for="subsection in section.subsecciones" :key="subsection.numero" class="subsection-group">
                    <h3 class="subsection-title">{{ subsection.numero }} {{ subsection.titulo }}</h3>
                    <p v-if="subsection.objetivo" class="section-objective">Objetivo: {{ subsection.objetivo }}</p>
                    <p v-if="subsection.introduccion && !subsection.sub_subsecciones">{{ subsection.introduccion }}</p>
                    <p v-if="subsection.descripcion">{{ subsection.descripcion }}</p>

                    <!-- Características de sistemas operativos (9.5) o aplicaciones (9.6) -->
                    <p v-if="subsection.caracteristicas_sistemas_operativos">{{
                        subsection.caracteristicas_sistemas_operativos }}</p>
                    <p v-if="subsection.caracteristicas_aplicaciones">{{ subsection.caracteristicas_aplicaciones }}</p>
                    <ul v-if="subsection.puntos_caracteristicas" class="styled-list">
                        <li v-for="(caract, index) in subsection.puntos_caracteristicas" :key="index">
                            <strong>{{ caract.letra }}</strong> {{ caract.item }}
                        </li>
                    </ul>

                    <!-- Controles/Prácticas (varias subsecciones) -->
                    <p v-if="subsection.controles_considerar">{{ subsection.controles_considerar }}</p>
                    <p v-if="subsection.controles_aplicar">{{ subsection.controles_aplicar }}</p>
                    <ul v-if="subsection.puntos_controles" class="styled-list">
                        <li v-for="(punto, index) in subsection.puntos_controles" :key="index">
                            <strong>{{ punto.letra }}</strong> {{ punto.item }}
                            <ul v-if="punto.subpuntos" class="sub-styled-list">
                                <li v-for="(subpunto, subIndex) in punto.subpuntos" :key="subIndex">
                                    {{ subpunto }}
                                </li>
                            </ul>
                        </li>
                    </ul>

                    <ul v-if="subsection.puntos_practica" class="styled-list">
                        <li v-for="(punto, index) in subsection.puntos_practica" :key="index">
                            <strong>{{ punto.letra }}</strong> {{ punto.item }}
                        </li>
                    </ul>

                    <!-- Consideraciones específicas (9.2.2, 9.4.2, 9.4.6, 9.6.2) -->
                    <p
                        v-if="subsection.consideraciones && (subsection.numero === '9.2.2' || subsection.numero === '9.4.2' || subsection.numero === '9.4.6' || subsection.numero === '9.6.2')">
                        {{ subsection.consideraciones }}</p>
                    <ul v-if="subsection.puntos_consideraciones && (subsection.numero === '9.2.2' || subsection.numero === '9.4.2' || subsection.numero === '9.4.6' || subsection.numero === '9.6.2')"
                        class="styled-list">
                        <li v-for="(punto, index) in subsection.puntos_consideraciones" :key="index">
                            <strong>{{ punto.letra }}</strong> {{ punto.item }}
                        </li>
                    </ul>

                    <!-- Gestión de claves 9.5.3 -->
                    <p v-if="subsection.descripcion && subsection.numero === '9.5.3'">{{ subsection.descripcion }}</p>

                    <!-- Monitoreo de uso del sistema 9.7 -->
                    <p v-if="subsection.descripcion && subsection.numero === '9.7'">{{ subsection.descripcion }}</p>
                    <p v-if="subsection.registros_incluir">{{ subsection.registros_incluir }}</p>
                    <ul v-if="subsection.puntos_registros" class="styled-list">
                        <li v-for="(punto, index) in subsection.puntos_registros" :key="index">
                            <strong>{{ punto.letra }}</strong> {{ punto.item }}
                        </li>
                    </ul>
                    <p v-if="subsection.consideracion_adicional">{{ subsection.consideracion_adicional }}</p>

                    <p v-if="subsection.importancia_sincronizacion">{{ subsection.importancia_sincronizacion }}</p>
                    <p v-if="subsection.estandar_acordado">{{ subsection.estandar_acordado }}</p>

                    <!-- Sub-subsecciones para 9.7.2 Monitoreo del uso del sistema -->
                    <div v-for="subSub in subsection.sub_subsecciones" :key="subSub.numero"
                        class="sub-subsection-group">
                        <h4 class="sub-subsection-title">{{ subSub.numero }} {{ subSub.titulo }}</h4>
                        <p v-if="subSub.introduccion">{{ subSub.introduccion }}</p>

                        <!-- Áreas a incluir 9.7.2.1 -->
                        <ul v-if="subSub.areas_incluir" class="styled-list">
                            <li v-for="(area, index) in subSub.areas_incluir" :key="index">
                                <strong>{{ area.letra }}</strong> {{ area.item }}
                                <ul v-if="area.subpuntos" class="sub-styled-list">
                                    <li v-for="(subpunto, subIndex) in area.subpuntos" :key="subIndex">{{ subpunto }}
                                    </li>
                                </ul>
                            </li>
                        </ul>

                        <!-- Factores de riesgo 9.7.2.2 -->
                        <p v-if="subSub.factores_riesgo">{{ subSub.factores_riesgo }}</p>
                        <ul v-if="subSub.puntos_factores" class="styled-list">
                            <li v-for="(factor, index) in subSub.puntos_factores" :key="index">
                                <strong>{{ factor.letra }}</strong> {{ factor.item }}
                            </li>
                        </ul>

                        <!-- Registro y revisión de eventos 9.7.2.3 -->
                        <p v-if="subSub.manejo_registros">{{ subSub.manejo_registros }}</p>
                        <p v-if="subSub.separacion_roles">{{ subSub.separacion_roles }}</p>
                        <p v-if="subSub.atencion_seguridad_registros">{{ subSub.atencion_seguridad_registros }}</p>
                        <ul v-if="subSub.problemas_operacionales" class="styled-list">
                            <li v-for="(problema, index) in subSub.problemas_operacionales" :key="index">
                                <strong>{{ problema.letra }}</strong> {{ problema.item }}
                            </li>
                        </ul>
                    </div>

                    <!-- Computadores móviles y teletrabajo 9.8 -->
                    <p v-if="subsection.uso_lugares_publicos">{{ subsection.uso_lugares_publicos }}</p>
                    <p v-if="subsection.evitar_observacion">{{ subsection.evitar_observacion }}</p>
                    <p v-if="subsection.proteccion_redes">{{ subsection.proteccion_redes }}</p>
                    <p v-if="subsection.proteccion_fisica">{{ subsection.proteccion_fisica }}</p>
                    <p v-if="subsection.entrenamiento_personal">{{ subsection.entrenamiento_personal }}</p>

                    <p v-if="subsection.autorizacion_control">{{ subsection.autorizacion_control }}</p>
                    <p v-if="subsection.desarrollo_politica">{{ subsection.desarrollo_politica }}</p>
                    <p v-if="subsection.consideraciones && subsection.numero === '9.8.2'">{{ subsection.consideraciones
                        }}</p>
                    <ul v-if="subsection.consideraciones && subsection.numero === '9.8.2'" class="styled-list">
                        <li v-for="(consideracion, index) in subsection.consideraciones" :key="index">
                            <strong>{{ consideracion.letra }}</strong> {{ consideracion.item }}
                        </li>
                    </ul>
                    <p v-if="subsection.controles_disposiciones">{{ subsection.controles_disposiciones }}</p>
                    <ul v-if="subsection.puntos_controles_disposiciones" class="styled-list">
                        <li v-for="(disposicion, index) in subsection.puntos_controles_disposiciones" :key="index">
                            <strong>{{ disposicion.letra }}</strong> {{ disposicion.item }}
                        </li>
                    </ul>

                </div>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Control de acceso"...</p>
    </div>
</template>

<style scoped>
/* Copia y pega los estilos generales de tus otras vistas aquí. */
.control-acceso-container {
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

.sub-subsection-group {
    margin-left: 15px;
    margin-bottom: 25px;
    padding-left: 10px;
    border-left: 2px dotted #ccc;
}

.sub-subsection-title {
    color: #5d5d5d;
    margin-top: 18px;
    margin-bottom: 8px;
    font-size: 1.3em;
    font-weight: 500;
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