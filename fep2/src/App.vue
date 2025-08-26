<script setup>
import { ref, onMounted } from 'vue';
import Navbar from './components/Navbar.vue';

// ====================================================================================
// IMPORTS DE VISTAS:
// Asegúrate de que estos nombres de importación coincidan exactamente
// con tus nombres de archivo .vue en la carpeta src/views/
// ====================================================================================
// Vistas NCh2777
import PreambuloView from './views/PreambuloView.vue';
import IntroView from './views/IntroView.vue';
import Alcance from './views/Alcance.vue'; // Asumo que corresponde a '1 Alcance y campo de aplicación'
import Terminos from './views/terminos.vue'; // Asumo que corresponde a '2 Términos y definiciones'
import Seguridad from './views/seguridad.vue'; // Asumo que corresponde a '3 Política de seguridad'
import SeguridadOrganizacional from './views/SeguridadOrganizacionalView.vue';
import ClasificacionYControlDeBienes from './views/ClasificacionYControlDeBienesView.vue';
import SeguridadDelPersonal from './views/SeguridadDelPersonalView.vue';
import SeguridadFisicaYDelAmbiente from './views/SeguridadFisicaYDelAmbienteView.vue';
import GestionOperacionesYComunicaciones from './views/GestionOperacionesYComunicacionesView.vue';
import ControlDeAcceso from './views/ControlDeAccesoView.vue';
// Importa aquí las vistas 10, 11 y 12 de NCh2777 cuando las hayas creado con sus respectivos nombres de archivo
// import DesarrolloYMantenimientoDeSistemasView from './views/DesarrolloYMantenimientoDeSistemasView.vue';
// import GestionDeLaContinuidadDelNegocioView from './views/GestionDeLaContinuidadDelNegocioView.vue';
// import CumplimientoView from './views/CumplimientoView.vue';

// Vistas TFEP-01/2025
import Capitulo1AntecedentesYMarcoNormativoView from './views/Capitulo1AntecedentesYMarcoNormativoView.vue';
import Capitulo2CondicionesGeneralesDelProcesoView from './views/Capitulo2CondicionesGeneralesDelProcesoView.vue';
// === ¡Nuevas vistas del TFEP Capítulo 3, 4 y 5! ===
import Capitulo3ParticipantesView from './views/Capitulo3ParticipantesView.vue'; // Corregido: Importa el componente real del Capítulo 3
import Capitulo4GarantiasView from './views/Capitulo4GarantiasView.vue';
import Capitulo5RequisitosAdministrativosView from './views/Capitulo5RequisitosAdministrativosView.vue';
import Capitulo6ObtencionDeBasesYComunicacionesView from './views/Capitulo6ObtencionDeBasesYComunicacionesView.vue';
import Capitulo7ConsultasYAclaracionesView from './views/Capitulo7ConsultasYAclaracionesView.vue';
import Capitulo8PresentacionesPreparatoriasView from './views/Capitulo8PresentacionesPreparatoriasView.vue';
import Capitulo9RecepcionYAperturaDeOfertasView from './views/Capitulo9RecepcionYAperturaDeOfertasView.vue';
// ... (imports existentes) ...
import Capitulo10ProcesoDeEvaluacionView from './views/Capitulo10ProcesoDeEvaluacionView.vue';
import Capitulo11EvaluacionTecnicaView from './views/Capitulo11EvaluacionTecnicaView.vue';
import Capitulo12EvaluacionEconomicaView from './views/Capitulo12EvaluacionEconomicaView.vue';
import Capitulo13EvaluacionFinalYAdjudicacionView from './views/Capitulo13EvaluacionFinalYAdjudicacionView.vue';
import Capitulo14EvaluacionAcademicaView from './views/Capitulo14EvaluacionAcademicaView.vue';

// ... (imports existentes) ...
import Capitulo15FormalizacionDelContratoView from './views/Capitulo15FormalizacionDelContratoView.vue';
import Capitulo16GestionContractualView from './views/Capitulo16GestionContractualView.vue';
import Capitulo17ObligacionesDelContratistaView from './views/Capitulo17ObligacionesDelContratistaView.vue';
import Capitulo18NivelesDeServicioYPenalidadesView from './views/Capitulo18NivelesDeServicioYPenalidadesView.vue';
import Capitulo19TerminoDelContratoView from './views/Capitulo19TerminoDelContratoView.vue';
import Capitulo20ConfidencialidadYPropiedadIntelectualView from './views/Capitulo20ConfidencialidadYPropiedadIntelectualView.vue';
import Capitulo21SolucionDeControversiasView from './views/Capitulo21SolucionDeControversiasView.vue';
import Capitulo22GestionDelCambioYCapacitacionView from './views/Capitulo22GestionDelCambioYCapacitacionView.vue';


// Vistas TFEP-01/2025 (Bases Técnicas)
import BtCapitulo1IntroduccionView from './views/BtCapitulo1IntroduccionView.vue';
import BtCapitulo2AntecedentesView from './views/BtCapitulo2AntecedentesView.vue';
// ====================================================================================

// Define la vista que se mostrará por defecto al cargar la aplicación
const currentViewId = ref('capitulo-1-antecedentes-y-marco-normativo'); // Puedes ajustar para iniciar en cualquier capítulo

// Función para cambiar la vista y actualizar el hash de la URL
const navigateTo = (viewId) => {
  currentViewId.value = viewId;
  window.location.hash = viewId; // Actualiza el hash para que la URL sea persistente
};

// Hook de ciclo de vida: se ejecuta cuando el componente se monta en el DOM
onMounted(() => {
  // Si la URL ya tiene un hash al cargar la página, usa ese ID de vista
  if (window.location.hash) {
    currentViewId.value = window.location.hash.substring(1); // Elimina el '#'
  }
  // Escucha los cambios en el hash de la URL (por ejemplo, al usar botones de atrás/adelante del navegador)
  window.addEventListener('hashchange', () => {
    currentViewId.value = window.location.hash.substring(1);
  });
});

// Función auxiliar para formatear los títulos de las secciones, especialmente para el placeholder
const formatTitle = (id) => {
  if (!id) return '';
  const titles = {
    // Títulos completos para NCh2777
    'preambulo': 'Preámbulo (NCh2777)',
    'introduccion': '0 Introducción (NCh2777)',
    'alcance-y-campo-de-aplicacion': '1 Alcance y campo de aplicación (NCh2777)',
    'terminos-y-definiciones': '2 Términos y definiciones (NCh2777)',
    'politica-de-seguridad': '3 Política de seguridad (NCh2777)',
    'seguridad-organizacional': '4 Seguridad organizacional (NCh2777)',
    'clasificacion-y-control-de-bienes': '5 Clasificación y control de bienes (NCh2777)',
    'seguridad-del-personal': '6 Seguridad del personal (NCh2777)',
    'seguridad-fisica-y-del-ambiente': '7 Seguridad física y del ambiente (NCh2777)',
    'gestion-de-las-operaciones-y-de-las-comunicaciones': '8 Gestión de las operaciones y de las comunicaciones (NCh2777)',
    'control-de-acceso': '9 Control de acceso (NCh2777)',
    'desarrollo-y-mantenimiento-de-sistemas': '10 Desarrollo y mantenimiento de sistemas (NCh2777)',
    'gestion-de-la-continuidad-del-negocio': '11 Gestión de la continuidad del negocio (NCh2777)',
    'cumplimiento': '12 Cumplimiento (NCh2777)',
    // Títulos completos para TFEP-01/2025
    'capitulo-1-antecedentes-y-marco-normativo': 'Capítulo 1: Antecedentes y Marco Normativo (TFEP-01/2025)',
    'capitulo-2-condiciones-generales-del-proceso': 'Capítulo 2: Condiciones Generales del Proceso (TFEP-01/2025)',
    // === ¡Nuevos títulos para los Capítulos 3, 4 y 5 del TFEP! ===
    'capitulo-3-participantes': 'Capítulo 3: Participantes (TFEP-01/2025)',
    'capitulo-4-garantias': 'Capítulo 4: Garantías (TFEP-01/2025)',
    'capitulo-5-requisitos-administrativos': 'Capítulo 5: Requisitos Administrativos (TFEP-01/2025)',
    'capitulo-6-obtencion-de-bases-y-comunicaciones': 'Capítulo 6: Obtención de Bases y Comunicaciones (TFEP-01/2025)',
    'capitulo-7-consultas-y-aclaraciones': 'Capítulo 7: Consultas y Aclaraciones (TFEP-01/2025)',
    'capitulo-8-presentaciones-preparatorias': 'Capítulo 8: Presentaciones Preparatorias (TFEP-01/2025)',
    'capitulo-9-recepcion-y-apertura-de-ofertas': 'Capítulo 9: Recepción y Apertura de Ofertas (TFEP-01/2025)',
    'capitulo-10-proceso-de-evaluacion': 'Capítulo 10: Proceso de Evaluación (TFEP-01/2025)',
    'capitulo-11-evaluacion-tecnica': 'Capítulo 11: Evaluación Técnica (TFEP-01/2025)',
    'capitulo-12-evaluacion-economica': 'Capítulo 12: Evaluación Económica (TFEP-01/2025)',
    'capitulo-13-evaluacion-final-y-adjudicacion': 'Capítulo 13: Evaluación Final y Adjudicación (TFEP-01/2025)',
    'capitulo-14-evaluacion-academica': 'Capítulo 14: Evaluación Académica (TFEP-01/2025)',
    'capitulo-15-formalizacion-del-contrato': 'Capítulo 15: Formalización del Contrato (TFEP-01/2025)',
    'capitulo-16-gestion-contractual': 'Capítulo 16: Gestión Contractual (TFEP-01/2025)',
    'capitulo-17-obligaciones-del-contratista': 'Capítulo 17: Obligaciones del Contratista (TFEP-01/2025)',
    'capitulo-18-niveles-de-servicio-y-penalidades': 'Capítulo 18: Niveles de Servicio y Penalidades (TFEP-01/2025)',
    'capitulo-19-termino-del-contrato': 'Capítulo 19: Término del Contrato (TFEP-01/2025)',
    'capitulo-20-confidencialidad-y-propiedad-intelectual': 'Capítulo 20: Confidencialidad y Propiedad Intelectual (TFEP-01/2025)',
    'capitulo-21-solucion-de-controversias': 'Capítulo 21: Solución de Controversias (TFEP-01/2025)',
    'capitulo-22-gestion-del-cambio-y-capacitacion': 'Capítulo 22: Gestión del Cambio y Capacitación (TFEP-01/2025)',
    'bt-capitulo-1-introduccion': 'Bases Técnicas - Capítulo 1: Introducción (TFEP-01/2025)',
    'bt-capitulo-2-antecedentes': 'Bases Técnicas - Capítulo 2: Antecedentes (TFEP-01/2025)'
  };
  // Intenta encontrar el título en el mapa, si no lo encuentra, formatea el ID a "Título de Ejemplo"
  return titles[id] || id.split('-').map(word => word.charAt(0).toUpperCase() + word.slice(1)).join(' ');
};
</script>

<template>
  <div id="app-layout">
    <!-- El Navbar se encarga de la navegación y resalta la vista activa -->
    <Navbar @navigate="navigateTo" :activeViewId="currentViewId" />

    <main class="content-area">
      <!-- ==================================================================================== -->
      <!-- RENDERIZADO CONDICIONAL DE LAS VISTAS -->
      <!-- Las vistas se renderizan según el `currentViewId` -->
      <!-- ==================================================================================== -->

      <!-- Vistas del documento TFEP-01/2025 -->
      <Capitulo1AntecedentesYMarcoNormativoView v-if="currentViewId === 'capitulo-1-antecedentes-y-marco-normativo'" />
      <Capitulo2CondicionesGeneralesDelProcesoView
        v-else-if="currentViewId === 'capitulo-2-condiciones-generales-del-proceso'" />
      <!-- === ¡Nuevas condiciones para Capítulos 3, 4 y 5 del TFEP! === -->
      <Capitulo3ParticipantesView v-else-if="currentViewId === 'capitulo-3-participantes'" />
      <Capitulo4GarantiasView v-else-if="currentViewId === 'capitulo-4-garantias'" />
      <Capitulo5RequisitosAdministrativosView v-else-if="currentViewId === 'capitulo-5-requisitos-administrativos'" />
      <Capitulo6ObtencionDeBasesYComunicacionesView
        v-else-if="currentViewId === 'capitulo-6-obtencion-de-bases-y-comunicaciones'" />
      <Capitulo7ConsultasYAclaracionesView v-else-if="currentViewId === 'capitulo-7-consultas-y-aclaraciones'" />
      <Capitulo8PresentacionesPreparatoriasView
        v-else-if="currentViewId === 'capitulo-8-presentaciones-preparatorias'" />
      <Capitulo9RecepcionYAperturaDeOfertasView
        v-else-if="currentViewId === 'capitulo-9-recepcion-y-apertura-de-ofertas'" />

      <Capitulo10ProcesoDeEvaluacionView v-else-if="currentViewId === 'capitulo-10-proceso-de-evaluacion'" />
      <Capitulo11EvaluacionTecnicaView v-else-if="currentViewId === 'capitulo-11-evaluacion-tecnica'" />
      <Capitulo12EvaluacionEconomicaView v-else-if="currentViewId === 'capitulo-12-evaluacion-economica'" />
      <Capitulo13EvaluacionFinalYAdjudicacionView
        v-else-if="currentViewId === 'capitulo-13-evaluacion-final-y-adjudicacion'" />
      <!-- ... (vistas existentes de TFEP) ... -->
      <Capitulo14EvaluacionAcademicaView v-else-if="currentViewId === 'capitulo-14-evaluacion-academica'" />
      <!-- ¡Nuevas vistas aquí! -->
      <Capitulo15FormalizacionDelContratoView v-else-if="currentViewId === 'capitulo-15-formalizacion-del-contrato'" />
      <Capitulo16GestionContractualView v-else-if="currentViewId === 'capitulo-16-gestion-contractual'" />
      <Capitulo17ObligacionesDelContratistaView
        v-else-if="currentViewId === 'capitulo-17-obligaciones-del-contratista'" />
      <Capitulo18NivelesDeServicioYPenalidadesView
        v-else-if="currentViewId === 'capitulo-18-niveles-de-servicio-y-penalidades'" />
      <Capitulo19TerminoDelContratoView v-else-if="currentViewId === 'capitulo-19-termino-del-contrato'" />
      <Capitulo20ConfidencialidadYPropiedadIntelectualView
        v-else-if="currentViewId === 'capitulo-20-confidencialidad-y-propiedad-intelectual'" />
      <Capitulo21SolucionDeControversiasView v-else-if="currentViewId === 'capitulo-21-solucion-de-controversias'" />
      <Capitulo22GestionDelCambioYCapacitacionView
        v-else-if="currentViewId === 'capitulo-22-gestion-del-cambio-y-capacitacion'" />
      <BtCapitulo1IntroduccionView v-else-if="currentViewId === 'bt-capitulo-1-introduccion'" /> <!-- ¡Nuevo! -->
      <BtCapitulo2AntecedentesView v-else-if="currentViewId === 'bt-capitulo-2-antecedentes'" /> <!-- ¡Nuevo! -->
      <!-- Vistas del documento NCh2777 -->
      <PreambuloView v-else-if="currentViewId === 'preambulo'" />
      <IntroView v-else-if="currentViewId === 'introduccion'" />
      <Alcance v-else-if="currentViewId === 'alcance-y-campo-de-aplicacion'" />
      <Terminos v-else-if="currentViewId === 'terminos-y-definiciones'" />
      <Seguridad v-else-if="currentViewId === 'politica-de-seguridad'" />
      <SeguridadOrganizacional v-else-if="currentViewId === 'seguridad-organizacional'" />
      <ClasificacionYControlDeBienes v-else-if="currentViewId === 'clasificacion-y-control-de-bienes'" />
      <SeguridadDelPersonal v-else-if="currentViewId === 'seguridad-del-personal'" />
      <SeguridadFisicaYDelAmbiente v-else-if="currentViewId === 'seguridad-fisica-y-del-ambiente'" />
      <GestionOperacionesYComunicaciones
        v-else-if="currentViewId === 'gestion-de-las-operaciones-y-de-las-comunicaciones'" />
      <ControlDeAcceso v-else-if="currentViewId === 'control-de-acceso'" />
      <!-- Agrega aquí los v-else-if para las vistas 10, 11 y 12 de NCh2777 cuando las tengas -->
      <!-- <DesarrolloYMantenimientoDeSistemasView v-else-if="currentViewId === 'desarrollo-y-mantenimiento-de-sistemas'" /> -->
      <!-- <GestionDeLaContinuidadDelNegocioView v-else-if="currentViewId === 'gestion-de-la-continuidad-del-negocio'" /> -->
      <!-- <CumplimientoView v-else-if="currentViewId === 'cumplimiento'" /> -->

      <!-- Placeholder genérico para vistas no implementadas o IDs desconocidos -->
      <div v-else class="placeholder-view">
        <h1 class="main-title">{{ formatTitle(currentViewId) }}</h1>
        <p>Contenido de la sección de "{{ formatTitle(currentViewId) }}" no implementada aún.</p>
        <p>
          Este visor permite consultar varios documentos. Selecciona una sección del menú lateral.
        </p>
      </div>
    </main>
  </div>
</template>

<style>
/* ==================================================================================== */
/* ESTILOS GLOBALES Y DE LAYOUT (sin "scoped" para que afecten a toda la aplicación) */
/* ==================================================================================== */
html,
body {
  margin: 0;
  padding: 0;
  height: 100%;
  /* Asegura que html y body ocupen toda la altura */
  overflow: hidden;
  /* Evita el scroll del body; el scroll lo gestionará `.content-area` */
}

body {
  font-family: 'Arial', sans-serif;
  background-color: #f0f2f5;
  /* Color de fondo general de la aplicación */
}

#app-layout {
  display: flex;
  /* Habilita Flexbox para el layout principal */
  min-height: 100vh;
  /* Asegura que el layout ocupe al menos la altura de la ventana */
  width: 100vw;
  /* Asegura que ocupe todo el ancho de la ventana */
  /* overflow-x: hidden; */
  /* Evita el scroll horizontal general si algún elemento lo causa */
}

.content-area {
  margin-left: 280px;
  /* Desplaza el contenido a la derecha del Navbar fijo (ancho del navbar) */
  flex-grow: 1;
  /* Permite que el área de contenido ocupe todo el espacio restante horizontal */
  padding: 30px;
  /* Espaciado interno para el contenido */
  box-sizing: border-box;
  /* Incluye el padding en el ancho/alto total */
  overflow-y: auto;
  /* Permite el scroll vertical solo en esta área si el contenido es largo */
  max-height: 100vh;
  /* Limita la altura del área de contenido para habilitar el scroll */
}

/* Estilos para el contenedor de vistas no implementadas (placeholder) */
.placeholder-view {
  padding: 30px;
  background-color: #ffffff;
  border-radius: 8px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
  text-align: center;
}

.placeholder-view .main-title {
  color: #7f8c8d;
  margin-bottom: 25px;
  border-bottom: 1px dashed #ccc;
  padding-bottom: 15px;
  font-size: 2em;
}

.placeholder-view p {
  line-height: 1.6;
  color: #666;
  margin-bottom: 15px;
}
</style>