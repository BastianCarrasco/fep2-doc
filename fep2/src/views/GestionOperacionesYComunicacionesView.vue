<script setup>
import { ref, onMounted } from 'vue';

const gestionOperacionesData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textos/gestion-operaciones-comunicaciones.json'); // Ajusta la ruta
        gestionOperacionesData.value = response.default;
    } catch (error) {
        console.error('Error al cargar la sección "Gestión de las operaciones y de las comunicaciones":', error);
        errorMessage.value = 'No se pudo cargar la información de "Gestión de las operaciones y de las comunicaciones".';
    }
});
</script>

<template>
    <div class="gestion-operaciones-container">
        <h1 class="main-title" v-if="gestionOperacionesData">{{ gestionOperacionesData.titulo_seccion }}</h1>

        <div v-if="gestionOperacionesData && gestionOperacionesData.secciones" class="content">
            <div v-for="section in gestionOperacionesData.secciones" :key="section.numero" class="section-group">
                <h2 class="section-title">{{ section.numero }} {{ section.titulo }}</h2>
                <p v-if="section.objetivo" class="section-objective">Objetivo: {{ section.objetivo }}</p>
                <p v-if="section.introduccion && section.numero === '8.5'">{{ section.introduccion }}</p>
                <p v-if="section.acuerdos_base">{{ section.acuerdos_base }}</p>

                <div v-for="subsection in section.subsecciones" :key="subsection.numero" class="subsection-group">
                    <h3 class="subsection-title">{{ subsection.numero }} {{ subsection.titulo }}</h3>
                    <p v-if="subsection.objetivo" class="section-objective">Objetivo: {{ subsection.objetivo }}</p>
                    <p v-if="subsection.parrafo_introductorio">{{ subsection.parrafo_introductorio }}</p>
                    <p v-if="subsection.introduccion && !subsection.sub_subsecciones">{{ subsection.introduccion }}</p>

                    <!-- Procedimientos de operaciones 8.1.1 -->
                    <ul v-if="subsection.procedimientos_incluir" class="styled-list">
                        <li v-for="(proc, index) in subsection.procedimientos_incluir" :key="index">{{ proc }}</li>
                    </ul>
                    <p v-if="subsection.revision_actualizacion">{{ subsection.revision_actualizacion }}</p>

                    <!-- Gestión de cambios 8.1.2 -->
                    <p v-if="subsection.controles_considerar && subsection.numero === '8.1.2'">{{
                        subsection.controles_considerar }}</p>
                    <ul v-if="subsection.puntos_controles && subsection.numero === '8.1.2'" class="styled-list">
                        <li v-for="(control, index) in subsection.puntos_controles" :key="index">
                            <strong>{{ control.letra }}</strong> {{ control.item }}
                        </li>
                    </ul>

                    <!-- Separación de obligaciones 8.1.3 -->
                    <p v-if="subsection.consideraciones && subsection.numero === '8.1.3'">{{ subsection.consideraciones
                        }}</p>
                    <p v-if="subsection.pequenas_organizaciones">{{ subsection.pequenas_organizaciones }}</p>
                    <p v-if="subsection.conflicto_intereses">{{ subsection.conflicto_intereses }}</p>

                    <!-- Separación de ambientes 8.1.4 -->
                    <p v-if="subsection.consideraciones && subsection.numero === '8.1.4'">{{ subsection.consideraciones
                        }}</p>
                    <ul v-if="subsection.puntos_consideraciones && subsection.numero === '8.1.4'" class="styled-list">
                        <li v-for="(punto, index) in subsection.puntos_consideraciones" :key="index">
                            <strong>{{ punto.letra }}</strong> {{ punto.item }}
                        </li>
                    </ul>

                    <!-- Aceptación del sistema 8.2.1 -->
                    <p v-if="subsection.consideraciones && subsection.numero === '8.2.1'">{{ subsection.consideraciones
                        }}</p>
                    <ul v-if="subsection.puntos_consideraciones && subsection.numero === '8.2.1'" class="styled-list">
                        <li v-for="(punto, index) in subsection.puntos_consideraciones" :key="index">
                            <strong>{{ punto.letra }}</strong> {{ punto.item }}
                        </li>
                    </ul>

                    <!-- Planificación de la capacidad 8.2.2 -->
                    <p v-if="subsection.consideraciones && subsection.numero === '8.2.2'">{{ subsection.consideraciones
                        }}</p>
                    <ul v-if="subsection.puntos_consideraciones && subsection.numero === '8.2.2'" class="styled-list">
                        <li v-for="(punto, index) in subsection.puntos_consideraciones" :key="index">
                            <strong>{{ punto.letra }}</strong> {{ punto.item }}
                        </li>
                    </ul>
                    <p v-if="subsection.impacto_seguridad">{{ subsection.impacto_seguridad }}</p>

                    <!-- Protección contra software malicioso 8.3 -->
                    <p v-if="subsection.consideraciones && subsection.numero === '8.3'">{{ subsection.consideraciones }}
                    </p>
                    <ul v-if="subsection.puntos_consideraciones && subsection.numero === '8.3'" class="styled-list">
                        <li v-for="(punto, index) in subsection.puntos_consideraciones" :key="index">
                            <strong>{{ punto.letra }}</strong> {{ punto.item }}
                            <ul v-if="punto.subpuntos" class="sub-styled-list">
                                <li v-for="(subpunto, subIndex) in punto.subpuntos" :key="subIndex">{{ subpunto }}</li>
                            </ul>
                        </li>
                    </ul>
                    <p v-if="subsection.nota">{{ subsection.nota }}</p>

                    <!-- Copias de respaldo 8.4.1 -->
                    <p v-if="subsection.controles_considerar && subsection.numero === '8.4.1'">{{
                        subsection.controles_considerar }}</p>
                    <ul v-if="subsection.puntos_controles && subsection.numero === '8.4.1'" class="styled-list">
                        <li v-for="(control, index) in subsection.puntos_controles" :key="index">
                            <strong>{{ control.letra }}</strong> {{ control.item }}
                        </li>
                    </ul>

                    <!-- Gestión de soporte de seguridad 8.4.2 -->
                    <p v-if="subsection.controles_considerar && subsection.numero === '8.4.2'">{{
                        subsection.controles_considerar }}</p>
                    <ul v-if="subsection.puntos_controles && subsection.numero === '8.4.2'" class="styled-list">
                        <li v-for="(control, index) in subsection.puntos_controles" :key="index">
                            <strong>{{ control.letra }}</strong> {{ control.item }}
                        </li>
                    </ul>

                    <!-- Controles de seguridad de red 8.5.1 -->
                    <p v-if="subsection.consideraciones && subsection.numero === '8.5.1'">{{ subsection.consideraciones
                        }}</p>
                    <ul v-if="subsection.puntos_consideraciones && subsection.numero === '8.5.1'" class="styled-list">
                        <li v-for="(punto, index) in subsection.puntos_consideraciones" :key="index">
                            <strong>{{ punto.letra }}</strong> {{ punto.item }}
                        </li>
                    </ul>

                    <!-- Gestión de dispositivos removibles 8.6.1 -->
                    <p v-if="subsection.controles_considerar && subsection.numero === '8.6.1'">{{
                        subsection.controles_considerar }}</p>
                    <ul v-if="subsection.puntos_controles && subsection.numero === '8.6.1'" class="styled-list">
                        <li v-for="(control, index) in subsection.puntos_controles" :key="index">
                            <strong>{{ control.letra }}</strong> {{ control.item }}
                        </li>
                    </ul>
                    <p v-if="subsection.nota && subsection.numero === '8.6.1'">{{ subsection.nota }}</p>

                    <!-- Eliminación de dispositivos y papeles en desuso 8.6.2 -->
                    <p v-if="subsection.controles_considerar && subsection.numero === '8.6.2'">{{
                        subsection.controles_considerar }}</p>
                    <ul v-if="subsection.puntos_controles && subsection.numero === '8.6.2'" class="styled-list">
                        <li v-for="(control, index) in subsection.puntos_controles" :key="index">
                            <template v-if="control.letra">
                                <strong>{{ control.letra }}</strong> {{ control.item }}
                            </template>
                            <template v-else>
                                <!-- Caso especial para b.1 a b.11 que están directamente en el nivel de subpuntos_g -->
                                <ul v-if="control.subpuntos_g" class="sub-styled-list">
                                    <li v-for="(sub, subIndex) in control.subpuntos_g" :key="subIndex">{{ sub }}</li>
                                </ul>
                            </template>
                        </li>
                    </ul>
                    <p v-if="subsection.efecto_agregado">{{ subsection.efecto_agregado }}</p>

                    <!-- Procedimientos de manipulación de la información 8.6.3 -->
                    <p v-if="subsection.controles_considerar && subsection.numero === '8.6.3'">{{
                        subsection.controles_considerar }}</p>
                    <ul v-if="subsection.puntos_controles && subsection.numero === '8.6.3'" class="styled-list">
                        <li v-for="(control, index) in subsection.puntos_controles" :key="index">
                            <strong>{{ control.letra }}</strong> {{ control.item }}
                        </li>
                    </ul>

                    <!-- Seguridad de la documentación de sistema 8.6.4 -->
                    <p v-if="subsection.controles_considerar && subsection.numero === '8.6.4'">{{
                        subsection.controles_considerar }}</p>
                    <ul v-if="subsection.puntos_controles && subsection.numero === '8.6.4'" class="styled-list">
                        <li v-for="(control, index) in subsection.puntos_controles" :key="index">
                            <strong>{{ control.letra }}</strong> {{ control.item }}
                        </li>
                    </ul>

                    <!-- Acuerdos de intercambio de información y software 8.7.1 -->
                    <p v-if="subsection.condiciones_seguridad">{{ subsection.condiciones_seguridad }}</p>
                    <ul v-if="subsection.puntos_condiciones" class="styled-list">
                        <li v-for="(punto, index) in subsection.puntos_condiciones" :key="index">
                            <strong>{{ punto.letra }}</strong> {{ punto.item }}
                        </li>
                    </ul>

                    <!-- Seguridad de los dispositivos en tránsito 8.7.2 -->
                    <p v-if="subsection.controles_aplicar">{{ subsection.controles_aplicar }}</p>
                    <ul v-if="subsection.puntos_controles && subsection.numero === '8.7.2'" class="styled-list">
                        <li v-for="(control, index) in subsection.puntos_controles" :key="index">
                            <strong>{{ control.letra }}</strong> {{ control.item }}
                            <ul v-if="control.subpuntos" class="sub-styled-list">
                                <li v-for="(subpunto, subIndex) in control.subpuntos" :key="subIndex">{{ subpunto }}
                                </li>
                            </ul>
                        </li>
                    </ul>

                    <!-- Seguridad en el comercio electrónico 8.7.3 -->
                    <p v-if="subsection.controles_considerar && subsection.numero === '8.7.3'">{{
                        subsection.controles_considerar }}</p>
                    <ul v-if="subsection.puntos_controles && subsection.numero === '8.7.3'" class="styled-list">
                        <li v-for="(control, index) in subsection.puntos_controles" :key="index">
                            <strong>{{ control.letra }}</strong> {{ control.item }}
                        </li>
                    </ul>
                    <p v-if="subsection.consideraciones_criptograficas">{{ subsection.consideraciones_criptograficas }}
                    </p>
                    <p v-if="subsection.acuerdos_comerciales">{{ subsection.acuerdos_comerciales }}</p>
                    <p v-if="subsection.sistemas_publicos">{{ subsection.sistemas_publicos }}</p>
                    <p v-if="subsection.resistencia_ataques">{{ subsection.resistencia_ataques }}</p>

                    <!-- Sub-subsecciones para Seguridad del correo electrónico 8.7.4 -->
                    <div v-for="subSub in subsection.sub_subsecciones" :key="subSub.numero"
                        class="sub-subsection-group">
                        <h4 class="sub-subsection-title">{{ subSub.numero }} {{ subSub.titulo }}</h4>
                        <p v-if="subSub.introduccion">{{ subSub.introduccion }}</p>
                        <ul v-if="subSub.riesgos" class="styled-list">
                            <li v-for="(riesgo, index) in subSub.riesgos" :key="index">
                                <strong>{{ riesgo.letra }}</strong> {{ riesgo.item }}
                            </li>
                        </ul>
                        <ul v-if="subSub.puntos_politica" class="styled-list">
                            <li v-for="(punto, index) in subSub.puntos_politica" :key="index">
                                <strong>{{ punto.letra }}</strong> {{ punto.item }}
                            </li>
                        </ul>
                    </div>

                    <!-- Seguridad de los sistemas de la oficina electrónica 8.7.5 -->
                    <p v-if="subsection.consideraciones_seguridad">{{ subsection.consideraciones_seguridad }}</p>
                    <ul v-if="subsection.puntos_consideraciones && subsection.numero === '8.7.5'" class="styled-list">
                        <li v-for="(punto, index) in subsection.puntos_consideraciones" :key="index">
                            <strong>{{ punto.letra }}</strong> {{ punto.item }}
                        </li>
                    </ul>

                    <!-- Sistemas disponibles públicamente 8.7.6 -->
                    <p v-if="subsection.proteccion_integridad">{{ subsection.proteccion_integridad }}</p>
                    <p v-if="subsection.cumplimiento_legal">{{ subsection.cumplimiento_legal }}</p>
                    <p v-if="subsection.proteccion_software_datos">{{ subsection.proteccion_software_datos }}</p>
                    <ul v-if="subsection.controles_publicacion_electronica" class="styled-list">
                        <li v-for="(control, index) in subsection.controles_publicacion_electronica" :key="index">
                            <strong>{{ control.letra }}</strong> {{ control.item }}
                        </li>
                    </ul>

                    <!-- Otras formas de intercambio de información 8.7.7 -->
                    <p v-if="subsection.procedimientos_controles">{{ subsection.procedimientos_controles }}</p>
                    <p v-if="subsection.compromiso_informacion">{{ subsection.compromiso_informacion }}</p>
                    <p v-if="subsection.interrupcion_negocio">{{ subsection.interrupcion_negocio }}</p>
                    <p v-if="subsection.declaracion_politica">{{ subsection.declaracion_politica }}</p>
                    <ul v-if="subsection.puntos_politica && subsection.numero === '8.7.7'" class="styled-list">
                        <li v-for="(punto, index) in subsection.puntos_politica" :key="index">
                            <strong>{{ punto.letra }}</strong> {{ punto.item }}
                            <ul v-if="punto.subpuntos" class="sub-styled-list">
                                <li v-for="(subpunto, subIndex) in punto.subpuntos" :key="subIndex">{{ subpunto }}</li>
                            </ul>
                        </li>
                    </ul>
                </div>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Gestión de las operaciones y de las comunicaciones"...</p>
    </div>
</template>

<style scoped>
/* Copia y pega los estilos generales de tus otras vistas aquí. */
.gestion-operaciones-container {
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