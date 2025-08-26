<script setup>
import { ref, onMounted } from 'vue';

const seguridadOrganizacionalData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textos/seguridad-organizacional.json'); // Ajusta la ruta a tu archivo JSON
        seguridadOrganizacionalData.value = response.default;
    } catch (error) {
        console.error('Error al cargar la sección "Seguridad organizacional":', error);
        errorMessage.value = 'No se pudo cargar la información de "Seguridad organizacional".';
    }
});

// Función para renderizar puntos con letras si existen
const renderNumberedList = (items) => {
    if (!items || items.length === 0) return null;
    return items.map(item => {
        let text = '';
        if (item.letra) {
            text += `<strong>${item.letra}</strong> `;
        }
        text += item.item;
        return text;
    }).filter(Boolean);
};
</script>

<template>
    <div class="seguridad-organizacional-container">
        <h1 class="main-title" v-if="seguridadOrganizacionalData">{{ seguridadOrganizacionalData.titulo_seccion }}</h1>

        <div v-if="seguridadOrganizacionalData && seguridadOrganizacionalData.secciones" class="content">
            <div v-for="section in seguridadOrganizacionalData.secciones" :key="section.numero" class="section-group">
                <h2 class="section-title">{{ section.numero }} {{ section.titulo }}</h2>
                <p v-if="section.objetivo" class="section-objective">Objetivo: {{ section.objetivo }}</p>
                <p v-if="section.control_acceso">{{ section.control_acceso }}</p>
                <p v-if="section.evaluacion_riesgos">{{ section.evaluacion_riesgos }}</p>
                <p v-if="section.otros_participantes">{{ section.otros_participantes }}</p>
                <p v-if="section.base_contratos">{{ section.base_contratos }}</p>
                <p v-if="section.disposiciones_contrato">{{ section.disposiciones_contrato }}</p>


                <div v-for="subsection in section.subsecciones" :key="subsection.numero" class="subsection-group">
                    <h3 class="subsection-title">{{ subsection.numero }} {{ subsection.titulo }}</h3>
                    <p v-if="subsection.parrafo_introductorio">{{ subsection.parrafo_introductorio }}</p>
                    <p v-if="subsection.introduccion">{{ subsection.introduccion }}</p>
                    <p v-if="subsection.promocion_seguridad">{{ subsection.promocion_seguridad }}</p>

                    <ul v-if="subsection.funciones_comite" class="styled-list">
                        <li v-for="(punto, index) in subsection.funciones_comite" :key="index">
                            <strong>{{ punto.letra }}</strong> {{ punto.item }}
                        </li>
                    </ul>

                    <p v-if="subsection.responsable_general">{{ subsection.responsable_general }}</p>
                    <p v-if="subsection.guia_general">{{ subsection.guia_general }}</p>
                    <p v-if="subsection.encargado_seguridad">{{ subsection.encargado_seguridad }}</p>
                    <p v-if="subsection.responsabilidad_directivos_dueños">{{
                        subsection.responsabilidad_directivos_dueños }}</p>
                    <p v-if="subsection.delegacion_responsabilidades">{{ subsection.delegacion_responsabilidades }}</p>

                    <p v-if="subsection.areas_responsabilidad_esenciales">{{ subsection.areas_responsabilidad_esenciales
                        }}</p>
                    <ul v-if="subsection.puntos_esenciales" class="styled-list">
                        <li v-for="(punto, index) in subsection.puntos_esenciales" :key="index">
                            <strong>{{ punto.letra }}</strong> {{ punto.item }}
                        </li>
                    </ul>

                    <p v-if="subsection.controles_considerar">{{ subsection.controles_considerar }}</p>
                    <ul v-if="subsection.puntos_controles" class="styled-list">
                        <li v-for="(punto, index) in subsection.puntos_controles" :key="index">
                            <strong>{{ punto.letra }}</strong> {{ punto.item }}
                        </li>
                    </ul>
                    <p v-if="subsection.nota_b" class="note-text">{{ subsection.nota_b }}</p>
                    <p v-if="subsection.importancia_red">{{ subsection.importancia_red }}</p>

                    <p v-if="subsection.necesidad_consejo">{{ subsection.necesidad_consejo }}</p>
                    <p v-if="subsection.organizaciones_pequenas">{{ subsection.organizaciones_pequenas }}</p>
                    <p v-if="subsection.mision_asesores">{{ subsection.mision_asesores }}</p>
                    <p v-if="subsection.consulta_incidentes">{{ subsection.consulta_incidentes }}</p>

                    <p v-if="subsection.contactos_apropiados">{{ subsection.contactos_apropiados }}</p>
                    <p v-if="subsection.restriccion_informacion">{{ subsection.restriccion_informacion }}</p>
                    <p v-if="subsection.quien_realiza_revision">{{ subsection.quien_realiza_revision }}</p>

                    <!-- Sub-subsecciones para 4.2.1 -->
                    <div v-for="subSub in subsection.sub_subsecciones" :key="subSub.numero"
                        class="sub-subsection-group">
                        <h4 class="sub-subsection-title">{{ subSub.numero }} {{ subSub.titulo }}</h4>
                        <p v-if="subSub.introduccion">{{ subSub.introduccion }}</p>

                        <ul v-if="subSub.tipos" class="styled-list">
                            <li v-for="(tipo, index) in subSub.tipos" :key="index">
                                <strong>{{ tipo.letra }}</strong> {{ tipo.item }}
                            </li>
                        </ul>
                        <ul v-if="subSub.ejemplos" class="styled-list">
                            <li v-for="(ejemplo, index) in subSub.ejemplos" :key="index">
                                <strong>{{ ejemplo.letra }}</strong> {{ ejemplo.item }}
                            </li>
                        </ul>
                        <p v-if="subSub.riesgo_informacion">{{ subSub.riesgo_informacion }}</p>
                        <p v-if="subSub.controles_necesarios">{{ subSub.controles_necesarios }}</p>
                        <p v-if="subSub.autorizacion_acceso">{{ subSub.autorizacion_acceso }}</p>

                        <ul v-if="subSub.ejemplos_personal_externo" class="styled-list">
                            <li v-for="(ejemplo, index) in subSub.ejemplos_personal_externo" :key="index">
                                <strong>{{ ejemplo.letra }}</strong> {{ ejemplo.item }}
                            </li>
                        </ul>
                    </div>

                    <!-- Términos de Contrato para 4.2.2 -->
                    <p v-if="subsection.indemnizacion">{{ subsection.indemnizacion }}</p>
                    <ul v-if="subsection.terminos_contrato" class="styled-list">
                        <li v-for="(termino, index) in subsection.terminos_contrato" :key="index">
                            <strong>{{ termino.letra }}</strong> {{ termino.item }}
                            <ul v-if="termino.subpuntos" class="sub-styled-list">
                                <li v-for="(subpunto, subIndex) in termino.subpuntos" :key="subIndex">
                                    {{ subpunto }}
                                </li>
                            </ul>
                        </li>
                    </ul>

                    <!-- Contratos de Externalización 4.3.1 -->
                    <p v-if="subsection.ejemplos_contrato">{{ subsection.ejemplos_contrato }}</p>
                    <ul v-if="subsection.puntos_ejemplos" class="styled-list">
                        <li v-for="(ejemplo, index) in subsection.puntos_ejemplos" :key="index">
                            <strong>{{ ejemplo.letra }}</strong> {{ ejemplo.item }}
                        </li>
                    </ul>
                    <p v-if="subsection.consideraciones_adicionales">{{ subsection.consideraciones_adicionales }}</p>
                    <p v-if="subsection.punto_de_partida">{{ subsection.punto_de_partida }}</p>
                </div>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Seguridad organizacional"...</p>
    </div>
</template>

<style scoped>
/* Estilos generales (pueden copiarse de otras vistas) */
.seguridad-organizacional-container {
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

/* Clases para los diferentes niveles de títulos y agrupaciones */
.section-group {
    margin-bottom: 45px;
    border-left: 4px solid #007bff;
    /* Barra más prominente para secciones principales */
    padding-left: 20px;
}

.section-title {
    color: #007bff;
    margin-top: 35px;
    margin-bottom: 15px;
    font-size: 2em;
    /* Título de sección más grande */
    font-weight: bold;
    position: relative;
    padding-left: 0;
    /* No necesitamos padding-left adicional aquí si ya hay un border-left */
}

/* Opcional: Remueve el bullet del section-title si la barra ya es suficiente */
.section-title::before {
    content: '';
    /* Quitamos el bullet si hay una barra lateral */
}

.section-objective {
    font-style: italic;
    color: #6a737d;
    margin-top: -10px;
    /* Para que quede más cerca del título */
    margin-bottom: 20px;
}

.subsection-group {
    margin-bottom: 30px;
    border-left: 3px solid #e0e0e0;
    padding-left: 15px;
    margin-top: 25px;
    /* Espacio superior para subsecciones */
}

.subsection-title {
    color: #4a4a4a;
    margin-top: 20px;
    margin-bottom: 10px;
    font-size: 1.6em;
    /* Título de subsección */
    font-weight: 600;
}

.sub-subsection-group {
    margin-left: 15px;
    /* Indentación para las sub-subsecciones */
    margin-bottom: 25px;
    padding-left: 10px;
    border-left: 2px dotted #ccc;
    /* Línea punteada para menor jerarquía */
}

.sub-subsection-title {
    color: #5d5d5d;
    margin-top: 18px;
    margin-bottom: 8px;
    font-size: 1.3em;
    font-weight: 500;
}


/* Estilos para párrafos, strong, listas y tablas */
p {
    margin-bottom: 10px;
    text-align: justify;
    /* Justificar texto para mejor lectura en bloques */
}

strong {
    color: #222;
}

.styled-list {
    list-style: none;
    /* Quitamos el estilo de disco predeterminado */
    margin-left: 0;
    margin-bottom: 15px;
    padding-left: 20px;
    /* Indentación para la lista principal */
}

.styled-list li {
    margin-bottom: 8px;
    line-height: 1.5;
    color: #555;
    position: relative;
    padding-left: 10px;
    /* Espacio para el bullet/letra si es necesario */
}

/* Estilo para las letras (a), (b), etc. */
.styled-list li strong {
    margin-right: 5px;
    /* Espacio entre la letra y el texto */
    color: #007bff;
    /* Color de acento para las letras */
}

.sub-styled-list {
    list-style: disc;
    /* Vuelve a usar disco para las sublistas */
    margin-left: 25px;
    /* Indenta la sublista */
    margin-top: 5px;
    margin-bottom: 5px;
}

.sub-styled-list li {
    margin-bottom: 5px;
    line-height: 1.4;
    color: #666;
}

.note-text {
    font-style: italic;
    color: #888;
    margin-top: 15px;
    margin-left: 15px;
    /* Indentar la nota */
    border-left: 2px solid #ddd;
    padding-left: 10px;
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