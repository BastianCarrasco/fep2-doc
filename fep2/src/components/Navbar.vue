<script setup>
import { ref, defineEmits, defineProps } from 'vue';

const emits = defineEmits(['navigate']);
const props = defineProps({
    activeViewId: {
        type: String,
        default: 'capitulo-1-antecedentes-y-marco-normativo' // Puedes ajustar el ID de la vista inicial aquí
    }
});

const mainSections = ref([
    { type: 'header', title: 'Bases de Licitación TFEP-01/2025' },
    { type: 'sub_header', title: 'TÍTULO I DISPOSICIONES GENERALES' },
    { id: 'capitulo-1-antecedentes-y-marco-normativo', title: 'Capítulo 1: Marco Normativo' },
    { id: 'capitulo-2-condiciones-generales-del-proceso', title: 'Capítulo 2: Condiciones Generales' },

    { type: 'sub_header', title: 'TÍTULO II REQUISITOS Y CONDICIONES DE PARTICIPACIÓN' },
    { id: 'capitulo-3-participantes', title: 'Capítulo 3: Participantes' },
    { id: 'capitulo-4-garantias', title: 'Capítulo 4: Garantías' },
    { id: 'capitulo-5-requisitos-administrativos', title: 'Capítulo 5: Requisitos Administrativos' },

    { type: 'sub_header', title: 'TÍTULO III PROCESO DE LICITACIÓN' },
    { id: 'capitulo-6-obtencion-de-bases-y-comunicaciones', title: 'Capítulo 6: Obtención de Bases y Comunicaciones' },
    { id: 'capitulo-7-consultas-y-aclaraciones', title: 'Capítulo 7: Consultas y Aclaraciones' },
    { id: 'capitulo-8-presentaciones-preparatorias', title: 'Capítulo 8: Presentaciones Preparatorias' },
    { id: 'capitulo-9-recepcion-y-apertura-de-ofertas', title: 'Capítulo 9: Recepción y Apertura de Ofertas' },

    { type: 'sub_header', title: 'TÍTULO IV EVALUACIÓN Y ADJUDICACIÓN' },
    { id: 'capitulo-10-proceso-de-evaluacion', title: 'Capítulo 10: Proceso de Evaluación' },
    { id: 'capitulo-11-evaluacion-tecnica', title: 'Capítulo 11: Evaluación Técnica' },
    { id: 'capitulo-12-evaluacion-economica', title: 'Capítulo 12: Evaluación Económica' },
    { id: 'capitulo-13-evaluacion-final-y-adjudicacion', title: 'Capítulo 13: Evaluación Final y Adjudicación' },
    { id: 'capitulo-14-evaluacion-academica', title: 'Capítulo 14: Evaluación Académica' },

    { type: 'sub_header', title: 'TÍTULO V CONTRATACIÓN Y EJECUCIÓN' },
    { id: 'capitulo-15-formalizacion-del-contrato', title: 'Capítulo 15: Formalización del Contrato' },
    { id: 'capitulo-16-gestion-contractual', title: 'Capítulo 16: Gestión Contractual' },
    { id: 'capitulo-17-obligaciones-del-contratista', title: 'Capítulo 17: Obligaciones del Contratista' },
    { id: 'capitulo-18-niveles-de-servicio-y-penalidades', title: 'Capítulo 18: Niveles de Servicio y Penalidades' },
    { id: 'capitulo-19-termino-del-contrato', title: 'Capítulo 19: Término del Contrato' },

    { type: 'sub_header', title: 'TÍTULO VI DISPOSICIONES ESPECIALES' },
    { id: 'capitulo-20-confidencialidad-y-propiedad-intelectual', title: 'Capítulo 20: Confidencialidad y Propiedad Intelectual' },
    { id: 'capitulo-21-solucion-de-controversias', title: 'Capítulo 21: Solución de Controversias' },
    { id: 'capitulo-22-gestion-del-cambio-y-capacitacion', title: 'Capítulo 22: Gestión del Cambio y Capacitación' },

    { type: 'divider' }, /* Separador entre Bases Administrativas y Bases Técnicas */

    { type: 'header', title: 'Bases Técnicas TFEP-01/2025' },
    { id: 'bt-capitulo-1-introduccion', title: 'Capítulo 1: Introducción' },
    { id: 'bt-capitulo-2-antecedentes', title: 'Capítulo 2: Antecedentes' },
    { id: 'bt-capitulo-3-requerimientos-generales', title: 'Capítulo 3: Requerimientos Generales' },
    { id: 'bt-capitulo-4-instalaciones-y-usuarios', title: 'Capítulo 4: Instalaciones y Usuarios' },
    { id: 'bt-capitulo-5-problemas-actuales', title: 'Capítulo 5: Problemas Actuales' },
    { id: 'bt-capitulo-6-expectativas-de-la-nueva-solucion', title: 'Capítulo 6: Expectativas de la Nueva Solución' },
    { id: 'bt-capitulo-7-infraestructura-actual', title: 'Capítulo 7: Infraestructura Actual' },
    { id: 'bt-capitulo-8-requerimientos-del-proceso', title: 'Capítulo 8: Requerimientos del Proceso' },
    { id: 'bt-capitulo-9-requerimientos-tecnicos-funcionales-y-no-funcionales', title: 'Capítulo 9: Requerimientos Técnicos, Funcionales y No Funcionales' },
    { id: 'bt-capitulo-10-requerimientos-de-la-propuesta', title: 'Capítulo 10: Requerimientos de la Propuesta' },
    { id: 'bt-capitulo-11-planificacion', title: 'Capítulo 11: Planificación' },
    { id: 'bt-capitulo-12-caracteristicas-del-site-principal-y-secundarios', title: 'Capítulo 12: Site Principal y Secundarios' },
    { id: 'bt-capitulo-13-modelo-de-operacion-mantencion-y-soporte', title: 'Capítulo 13: Operación, Mantención y Soporte' },
    { id: 'bt-capitulo-14-estructura-del-proyecto', title: 'Capítulo 14: Estructura del Proyecto' },
    { id: 'bt-capitulo-15-innovaciones', title: 'Capítulo 15: Innovaciones' },
    { id: 'bt-capitulo-16-informacion-corporativa-y-presencia-digital', title: 'Capítulo 16: Información Corporativa y Presencia Digital' },
    { id: 'bt-capitulo-17-video-de-presentacion-de-la-propuesta', title: 'Capítulo 17: Video de Presentación' },
    { id: 'bt-capitulo-18-prototipo-de-interfaz-y-diseno-ux-ui', title: 'Capítulo 18: Prototipo Interfaz y Diseño UX/UI' },

    { type: 'sub_header', title: 'ANEXOS Y FORMULARIOS' },
    { id: 'anexo-a-volumetria-actual-y-proyectada', title: 'Anexo A: Volumetría' },
    { id: 'anexo-b-definiciones-y-glosario', title: 'Anexo B: Glosario' },
    { id: 'formulario-a1-identificacion-del-proponente', title: 'Formulario A-1: Identificación del Proponente' },
    { id: 'formulario-a5-identificacion-de-documentos', title: 'Formulario A-5: Identificación de Documentos' },
    { id: 'formulario-t6-experiencia-del-proponente', title: 'Formulario T-6: Experiencia del Proponente' },
    { id: 'formulario-t7-contenido-de-la-propuesta-tecnica', title: 'Formulario T-7: Contenido Propuesta Técnica' },
    { id: 'formulario-t9-metodologia-administracion-y-gestion', title: 'Formulario T-9: Metodología Administración y Gestión' },
    { id: 'formulario-t10-metodologia-desarrollo', title: 'Formulario T-10: Metodología Desarrollo' },
    { id: 'formulario-t14-plan-de-trabajo-edt-y-carta-gantt', title: 'Formulario T-14: Plan de Trabajo, EDT y Carta Gantt' },
    { id: 'formulario-t15-plan-de-trabajos-nivelacion-recursos', title: 'Formulario T-15: Nivelación de Recursos' },
    { id: 'formulario-t16-plan-de-riesgos', title: 'Formulario T-16: Plan de Riesgos' },
    { id: 'formulario-t17-protocolo-de-aceptacion', title: 'Formulario T-17: Protocolo de Aceptación' },
    { id: 'formulario-t18-propuesta-de-implantacion-puesta-en-marcha', title: 'Formulario T-18: Propuesta de Implantación' },
    { id: 'formulario-t20-calendario-de-actividades', title: 'Formulario T-20: Calendario de Actividades' },
    { id: 'formulario-t21-evaluacion', title: 'Formulario T-21: Evaluación Técnica' },
    { id: 'formulario-t22-contenido-presentaciones-preparatorias', title: 'Formulario T-22: Presentaciones Preparatorias' },
    { id: 'formulario-e21-estructura-de-la-propuesta-economica', title: 'Formulario E-21: Propuesta Económica' },
    { id: 'formulario-e24-condiciones-y-parametros-oferta-economica', title: 'Formulario E-24: Parámetros Oferta Económica' },
    { id: 'formulario-e25-hitos-de-pago', title: 'Formulario E-25: Hitos de Pago' },
    { id: 'formulario-e26-rango-valores-perfiles-profesionales', title: 'Formulario E-26: Rangos Perfiles Profesionales' },


    { type: 'divider' }, /* Separador entre Bases TFEP y NCh2777 */

    { type: 'header', title: 'Documento NCh2777' },
    { id: 'preambulo', title: 'Preámbulo' },
    { id: 'introduccion', title: '0 Introducción' },
    { id: 'alcance-y-campo-de-aplicacion', title: '1 Alcance y campo de aplicación' },
    { id: 'terminos-y-definiciones', title: '2 Términos y definiciones' },
    { id: 'politica-de-seguridad', title: '3 Política de seguridad' },
    { id: 'seguridad-organizacional', title: '4 Seguridad organizacional' },
    { id: 'clasificacion-y-control-de-bienes', title: '5 Clasificación y control de bienes' },
    { id: 'seguridad-del-personal', title: '6 Seguridad del personal' },
    { id: 'seguridad-fisica-y-del-ambiente', title: '7 Seguridad física y del ambiente' },
    { id: 'gestion-de-las-operaciones-y-de-las-comunicaciones', title: '8 Gestión de las operaciones y de las comunicaciones' },
    { id: 'control-de-acceso', title: '9 Control de acceso' },
    { id: 'desarrollo-y-mantenimiento-de-sistemas', title: '10 Desarrollo y mantenimiento de sistemas' },
    { id: 'gestion-de-la-continuidad-del-negocio', title: '11 Gestión de la continuidad del negocio' },
    { id: 'cumplimiento', title: '12 Cumplimiento' }
]);
</script>

<template>
    <nav class="navbar">
        <div class="navbar-header">
            <h3 class="navbar-title">Visor de Documentos</h3>
        </div>
        <ul class="navbar-list">
            <template v-for="(section, index) in mainSections" :key="index">
                <!-- Encabezado de grupo de documentos (ej. "Bases de Licitación TFEP-01/2025") -->
                <li v-if="section.type === 'header'" class="navbar-group-header">
                    {{ section.title }}
                </li>
                <!-- Sub-encabezado para TÍTULOS (ej. "TÍTULO I DISPOSICIONES GENERALES") -->
                <li v-else-if="section.type === 'sub_header'" class="navbar-sub-group-header">
                    {{ section.title }}
                </li>
                <!-- Separador visual entre grupos de documentos -->
                <li v-else-if="section.type === 'divider'" class="navbar-divider"></li>
                <!-- Elemento de navegación real (enlace a un capítulo/sección) -->
                <li v-else class="navbar-item">
                    <a :href="`#${section.id}`"
                        :class="['navbar-link', { 'active': section.id === props.activeViewId }]"
                        @click="handleClick($event, section.id)">
                        {{ section.title }}
                    </a>
                </li>
            </template>
        </ul>
    </nav>
</template>

<style scoped>
/* Estilos del contenedor principal del Navbar */
.navbar {
    width: 280px;
    background-color: #2c3e50;
    padding: 0;
    box-shadow: 3px 0 10px rgba(0, 0, 0, 0.2);
    position: fixed;
    height: 100%;
    overflow-y: auto;
    color: #ecf0f1;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    z-index: 1000;
}

/* Estilos del encabezado superior del Navbar */
.navbar-header {
    padding: 20px;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
    margin-bottom: 10px;
}

.navbar-title {
    color: #ffffff;
    font-size: 1.4em;
    margin: 0;
    text-align: center;
}

/* Estilos de la lista de navegación */
.navbar-list {
    list-style: none;
    padding: 10px 0;
    margin: 0;
}

/* Estilos para los encabezados de grupo de documentos (ej. "Documento TFEP-01/2025") */
.navbar-group-header {
    color: #00bcd4;
    /* Cian vibrante */
    font-weight: bold;
    padding: 15px 20px 5px 20px;
    font-size: 1.1em;
    text-transform: uppercase;
    margin-top: 15px;
    border-bottom: 1px dashed rgba(255, 255, 255, 0.05);
    margin-bottom: 5px;
}

/* Estilos para los sub-encabezados (TÍTULOS dentro de Bases Administrativas/Técnicas) */
.navbar-sub-group-header {
    color: #a0a0a0;
    /* Gris más suave */
    font-weight: 600;
    padding: 10px 20px 5px 25px;
    /* Ligeramente más indentado */
    font-size: 0.9em;
    text-transform: uppercase;
    margin-top: 10px;
    margin-bottom: 5px;
    border-left: 3px solid #555;
    /* Barra lateral más discreta */
}

/* Estilos para el separador visual entre grupos */
.navbar-divider {
    border-top: 1px solid rgba(255, 255, 255, 0.1);
    margin: 15px 20px;
}

/* Estilos para cada ítem de la lista de navegación */
.navbar-item {
    margin-bottom: 5px;
}

/* Estilos del enlace de navegación */
.navbar-link {
    text-decoration: none;
    color: #ecf0f1;
    font-weight: 500;
    padding: 10px 20px;
    display: block;
    border-radius: 0;
    transition: background-color 0.3s ease, color 0.3s ease;
    font-size: 0.95em;
    padding-left: 35px;
    /* Mayor indentación para los enlaces de capítulo */
}

/* Efecto hover en los enlaces */
.navbar-link:hover {
    background-color: #34495e;
    color: #ffffff;
}

/* Estilo del enlace activo (la sección actualmente visible) */
.navbar-link.active {
    background-color: #007bff;
    color: #ffffff;
    font-weight: bold;
    position: relative;
}

/* Indicador lateral para el elemento activo */
.navbar-link.active::before {
    content: '';
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    width: 5px;
    background-color: #00bcd4;
    border-radius: 0 3px 3px 0;
}
</style>