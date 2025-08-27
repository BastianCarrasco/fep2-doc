<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import Navbar from './components/Navbar.vue';

// ====================================================================================
// IMPORTS DE VISTAS: Asegúrate que estos nombres coincidan exactamente con tus archivos .vue
// ====================================================================================

// --- Vistas NCh2777 ---
import PreambuloView from './views/PreambuloView.vue';
import IntroView from './views/IntroView.vue';
import Alcance from './views/Alcance.vue';
import Terminos from './views/terminos.vue';
import Seguridad from './views/seguridad.vue';
import SeguridadOrganizacional from './views/SeguridadOrganizacionalView.vue';
import ClasificacionYControlDeBienes from './views/ClasificacionYControlDeBienesView.vue';
import SeguridadDelPersonal from './views/SeguridadDelPersonalView.vue';
import SeguridadFisicaYDelAmbiente from './views/SeguridadFisicaYDelAmbienteView.vue';
import GestionOperacionesYComunicaciones from './views/GestionOperacionesYComunicacionesView.vue';
import ControlDeAcceso from './views/ControlDeAccesoView.vue';
// ... (Aquí irían los imports de NCh2777 para 10, 11, 12 si los creas) ...
// import DesarrolloYMantenimientoDeSistemasView from './views/DesarrolloYMantenimientoDeSistemasView.vue';
// import GestionDeLaContinuidadDelNegocioView from './views/GestionDeLaContinuidadDelNegocioView.vue';
// import CumplimientoView from './views/CumplimientoView.vue';

// --- Vistas TFEP-01/2025 (Bases Administrativas) ---
import Capitulo1AntecedentesYMarcoNormativoView from './views/Capitulo1AntecedentesYMarcoNormativoView.vue';
import Capitulo2CondicionesGeneralesDelProcesoView from './views/Capitulo2CondicionesGeneralesDelProcesoView.vue';
import Capitulo3ParticipantesView from './views/Capitulo3ParticipantesView.vue';
import Capitulo4GarantiasView from './views/Capitulo4GarantiasView.vue';
import Capitulo5RequisitosAdministrativosView from './views/Capitulo5RequisitosAdministrativosView.vue';
import Capitulo6ObtencionDeBasesYComunicacionesView from './views/Capitulo6ObtencionDeBasesYComunicacionesView.vue';
import Capitulo7ConsultasYAclaracionesView from './views/Capitulo7ConsultasYAclaracionesView.vue';
import Capitulo8PresentacionesPreparatoriasView from './views/Capitulo8PresentacionesPreparatoriasView.vue';
import Capitulo9RecepcionYAperturaDeOfertasView from './views/Capitulo9RecepcionYAperturaDeOfertasView.vue';
import Capitulo10ProcesoDeEvaluacionView from './views/Capitulo10ProcesoDeEvaluacionView.vue';
import Capitulo11EvaluacionTecnicaView from './views/Capitulo11EvaluacionTecnicaView.vue';
import Capitulo12EvaluacionEconomicaView from './views/Capitulo12EvaluacionEconomicaView.vue';
import Capitulo13EvaluacionFinalYAdjudicacionView from './views/Capitulo13EvaluacionFinalYAdjudicacionView.vue';
import Capitulo14EvaluacionAcademicaView from './views/Capitulo14EvaluacionAcademicaView.vue';
import Capitulo15FormalizacionDelContratoView from './views/Capitulo15FormalizacionDelContratoView.vue';
import Capitulo16GestionContractualView from './views/Capitulo16GestionContractualView.vue';
import Capitulo17ObligacionesDelContratistaView from './views/Capitulo17ObligacionesDelContratistaView.vue';
import Capitulo18NivelesDeServicioYPenalidadesView from './views/Capitulo18NivelesDeServicioYPenalidadesView.vue';
import Capitulo19TerminoDelContratoView from './views/Capitulo19TerminoDelContratoView.vue';
import Capitulo20ConfidencialidadYPropiedadIntelectualView from './views/Capitulo20ConfidencialidadYPropiedadIntelectualView.vue';
import Capitulo21SolucionDeControversiasView from './views/Capitulo21SolucionDeControversiasView.vue';
import Capitulo22GestionDelCambioYCapacitacionView from './views/Capitulo22GestionDelCambioYCapacitacionView.vue';

// --- Vistas TFEP-01/2025 (Bases Técnicas) ---
import BtCapitulo1IntroduccionView from './views/BtCapitulo1IntroduccionView.vue';
import BtCapitulo2AntecedentesView from './views/BtCapitulo2AntecedentesView.vue';
import BtCapitulo3RequerimientosGeneralesView from './views/BtCapitulo3RequerimientosGeneralesView.vue';
import BtCapitulo4InstalacionesYUsuariosView from './views/BtCapitulo4InstalacionesYUsuariosView.vue';
import BtCapitulo5ProblemasActualesView from './views/BtCapitulo5ProblemasActualesView.vue';
import BtCapitulo6ExpectativasDeLaNuevaSolucionView from './views/BtCapitulo6ExpectativasDeLaNuevaSolucionView.vue';
import BtCapitulo7InfraestructuraActualView from './views/BtCapitulo7InfraestructuraActualView.vue';
import BtCapitulo8RequerimientosDelProcesoView from './views/BtCapitulo8RequerimientosDelProcesoView.vue';
import BtCapitulo9RequerimientosTecnicosFuncionalesYNoFuncionalesView from './views/BtCapitulo9RequerimientosTecnicosFuncionalesYNoFuncionalesView.vue';
import BtCapitulo10RequerimientosDeLaPropuestaView from './views/BtCapitulo10RequerimientosDeLaPropuestaView.vue';
import BtCapitulo11PlanificacionView from './views/BtCapitulo11PlanificacionView.vue';
import BtCapitulo12CaracteristicasDelSitePrincipalYSecundariosView from './views/BtCapitulo12CaracteristicasDelSitePrincipalYSecundariosView.vue';
import BtCapitulo13ModeloDeOperacionMantencionYSoporteView from './views/BtCapitulo13ModeloDeOperacionMantencionYSoporteView.vue';
import BtCapitulo14EstructuraDelProyectoView from './views/BtCapitulo14EstructuraDelProyectoView.vue';
import BtCapitulo15InnovacionesView from './views/BtCapitulo15InnovacionesView.vue';
import BtCapitulo16InformacionCorporativaYPresenciaDigitalView from './views/BtCapitulo16InformacionCorporativaYPresenciaDigitalView.vue';
import BtCapitulo17VideoDePresentacionDeLaPropuestaView from './views/BtCapitulo17VideoDePresentacionDeLaPropuestaView.vue';
import BtCapitulo18PrototipoDeInterfazYDisenoUXUIView from './views/BtCapitulo18PrototipoDeInterfazYDisenoUXUIView.vue';

// --- Vistas TFEP-01/2025 (Anexos y Formularios) ---
import AnexoAVolumetriaActualYProyectadaView from './views/AnexoAVolumetriaActualYProyectadaView.vue';
import AnexoBDefinicionesYGlosarioView from './views/AnexoBDefinicionesYGlosarioView.vue';
import FormularioA1IdentificacionDelProponenteView from './views/FormularioA1IdentificacionDelProponenteView.vue';
import FormularioA5IdentificacionDeDocumentosView from './views/FormularioA5IdentificacionDeDocumentosView.vue';
import FormularioT6ExperienciaDelProponenteView from './views/FormularioT6ExperienciaDelProponenteView.vue';
import FormularioT7ContenidoDeLaPropuestaTecnicaView from './views/FormularioT7ContenidoDeLaPropuestaTecnicaView.vue';
import FormularioT9MetodologiaAdministracionYGestionView from './views/FormularioT9MetodologiaAdministracionYGestionView.vue';
import FormularioT10MetodologiaDesarrolloView from './views/FormularioT10MetodologiaDesarrolloView.vue';
import FormularioT14PlanDeTrabajoEdtYCartaGanttView from './views/FormularioT14PlanDeTrabajoEdtYCartaGanttView.vue';
import FormularioT15PlanDeTrabajosNivelacionRecursosView from './views/FormularioT15PlanDeTrabajosNivelacionRecursosView.vue';
import FormularioT16PlanDeRiesgosView from './views/FormularioT16PlanDeRiesgosView.vue';
import FormularioT17ProtocoloDeAceptacionView from './views/FormularioT17ProtocoloDeAceptacionView.vue';
import FormularioT18PropuestaDeImplantacionPuestaEnMarchaView from './views/FormularioT18PropuestaDeImplantacionPuestaEnMarchaView.vue';
import FormularioT20CalendarioDeActividadesView from './views/FormularioT20CalendarioDeActividadesView.vue';
import FormularioT21EvaluacionView from './views/FormularioT21EvaluacionView.vue';
import FormularioT22ContenidoPresentacionesPreparatoriasView from './views/FormularioT22ContenidoPresentacionesPreparatoriasView.vue';
import FormularioE21EstructuraDeLaPropuestaEconomicaView from './views/FormularioE21EstructuraDeLaPropuestaEconomicaView.vue';


// Define la vista que se mostrará por defecto al cargar la aplicación
const currentViewId = ref('capitulo-1-antecedentes-y-marco-normativo');

// Estado para controlar si el navbar está abierto/cerrado en móvil
const isNavbarOpen = ref(false);
// Estado para detectar si la pantalla es lo suficientemente pequeña para considerarse "móvil"
const isMobile = ref(window.innerWidth <= 768);

// Función para manejar el cambio de tamaño de ventana y actualizar `isMobile`
const handleResize = () => {
  isMobile.value = window.innerWidth <= 768;
  if (!isMobile.value) { // Si el tamaño vuelve a ser de escritorio, cierra el navbar móvil
    isNavbarOpen.value = false;
  }
};

// Función para cambiar la vista y actualizar el hash de la URL
const navigateTo = (viewId) => {
  currentViewId.value = viewId;
  window.location.hash = viewId;
  if (isMobile.value) { // Cierra el navbar móvil después de seleccionar una vista
    isNavbarOpen.value = false;
  }
};

// Función para alternar el estado de apertura/cierre del navbar móvil
const toggleNavbar = () => {
  isNavbarOpen.value = !isNavbarOpen.value;
};

// Hook de ciclo de vida: se ejecuta cuando el componente se monta en el DOM
onMounted(() => {
  // Inicializa la vista según el hash de la URL al cargar la página
  if (window.location.hash) {
    currentViewId.value = window.location.hash.substring(1);
  }
  // Escucha los cambios en el hash de la URL (para navegación con botones de atrás/adelante del navegador)
  window.addEventListener('hashchange', () => {
    currentViewId.value = window.location.hash.substring(1);
  });

  // Escucha los cambios de tamaño de ventana para ajustar el estado `isMobile`
  window.addEventListener('resize', handleResize);
});

// Hook de ciclo de vida: se ejecuta cuando el componente se desmonta del DOM
onUnmounted(() => {
  // Limpia el listener para evitar fugas de memoria
  window.removeEventListener('resize', handleResize);
});

// Función auxiliar para formatear los títulos de las secciones, usada principalmente por el placeholder
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

    // Títulos completos para TFEP-01/2025 (Bases Administrativas)
    'capitulo-1-antecedentes-y-marco-normativo': 'Capítulo 1: Antecedentes y Marco Normativo (TFEP-01/2025)',
    'capitulo-2-condiciones-generales-del-proceso': 'Capítulo 2: Condiciones Generales del Proceso (TFEP-01/2025)',
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

    // Títulos completos para TFEP-01/2025 (Bases Técnicas)
    'bt-capitulo-1-introduccion': 'Bases Técnicas - Capítulo 1: Introducción (TFEP-01/2025)',
    'bt-capitulo-2-antecedentes': 'Bases Técnicas - Capítulo 2: Antecedentes (TFEP-01/2025)',
    'bt-capitulo-3-requerimientos-generales': 'Bases Técnicas - Capítulo 3: Requerimientos Generales (TFEP-01/2025)',
    'bt-capitulo-4-instalaciones-y-usuarios': 'Bases Técnicas - Capítulo 4: Instalaciones y Usuarios (TFEP-01/2025)',
    'bt-capitulo-5-problemas-actuales': 'Bases Técnicas - Capítulo 5: Problemas Actuales (TFEP-01/2025)',
    'bt-capitulo-6-expectativas-de-la-nueva-solucion': 'Bases Técnicas - Capítulo 6: Expectativas de la Nueva Solución (TFEP-01/2025)',
    'bt-capitulo-7-infraestructura-actual': 'Bases Técnicas - Capítulo 7: Infraestructura Actual (TFEP-01/2025)',
    'bt-capitulo-8-requerimientos-del-proceso': 'Bases Técnicas - Capítulo 8: Requerimientos del Proceso (TFEP-01/2025)',
    'bt-capitulo-9-requerimientos-tecnicos-funcionales-y-no-funcionales': 'Bases Técnicas - Capítulo 9: Requerimientos Técnicos, Funcionales y No Funcionales (TFEP-01/2025)',
    'bt-capitulo-10-requerimientos-de-la-propuesta': 'Bases Técnicas - Capítulo 10: Requerimientos de la Propuesta (TFEP-01/2025)',
    'bt-capitulo-11-planificacion': 'Bases Técnicas - Capítulo 11: Planificación (TFEP-01/2025)',
    'bt-capitulo-12-caracteristicas-del-site-principal-y-secundarios': 'Bases Técnicas - Capítulo 12: Características del Site Principal y Secundarios (TFEP-01/2025)',
    'bt-capitulo-13-modelo-de-operacion-mantencion-y-soporte': 'Bases Técnicas - Capítulo 13: Modelo de Operación, Mantención y Soporte (TFEP-01/2025)',
    'bt-capitulo-14-estructura-del-proyecto': 'Bases Técnicas - Capítulo 14: Estructura del Proyecto (TFEP-01/2025)',
    'bt-capitulo-15-innovaciones': 'Bases Técnicas - Capítulo 15: Innovaciones (TFEP-01/2025)',
    'bt-capitulo-16-informacion-corporativa-y-presencia-digital': 'Bases Técnicas - Capítulo 16: Información Corporativa y Presencia Digital (TFEP-01/2025)',
    'bt-capitulo-17-video-de-presentacion-de-la-propuesta': 'Bases Técnicas - Capítulo 17: Video de Presentación de la Propuesta (TFEP-01/2025)',
    'bt-capitulo-18-prototipo-de-interfaz-y-diseno-ux-ui': 'Bases Técnicas - Capítulo 18: Prototipo de Interfaz y Diseño UX/UI (TFEP-01/2025)',

    // Títulos completos para TFEP-01/2025 (Anexos y Formularios)
    'anexo-a-volumetria-actual-y-proyectada': 'Anexo A: Volumetría Actual y Proyectada (TFEP-01/2025)',
    'anexo-b-definiciones-y-glosario': 'Anexo B: Definiciones y Glosario (TFEP-01/2025)',
    'formulario-a1-identificacion-del-proponente': 'Formulario A-1: Identificación del Proponente (TFEP-01/2025)',
    'formulario-a5-identificacion-de-documentos': 'Formulario A-5: Identificación de Documentos (TFEP-01/2025)',
    'formulario-t6-experiencia-del-proponente': 'Formulario T-6: Experiencia del Proponente (TFEP-01/2025)',
    'formulario-t7-contenido-de-la-propuesta-tecnica': 'Formulario T-7: Contenido Propuesta Técnica (TFEP-01/2025)',
    'formulario-t9-metodologia-administracion-y-gestion': 'Formulario T-9: Metodología Administración y Gestión (TFEP-01/2025)',
    'formulario-t10-metodologia-desarrollo': 'Formulario T-10: Metodología Desarrollo (TFEP-01/2025)',
    'formulario-t14-plan-de-trabajo-edt-y-carta-gantt': 'Formulario T-14: Plan de Trabajo, EDT y Carta Gantt (TFEP-01/2025)',
    'formulario-t15-plan-de-trabajos-nivelacion-recursos': 'Formulario T-15: Nivelación de Recursos (TFEP-01/2025)',
    'formulario-t16-plan-de-riesgos': 'Formulario T-16: Plan de Riesgos (TFEP-01/2025)',
    'formulario-t17-protocolo-de-aceptacion': 'Formulario T-17: Protocolo de Aceptación (TFEP-01/2025)',
    'formulario-t18-propuesta-de-implantacion-puesta-en-marcha': 'Formulario T-18: Propuesta de Implantación (TFEP-01/2025)',
    'formulario-t20-calendario-de-actividades': 'Formulario T-20: Calendario de Actividades (TFEP-01/2025)',
    'formulario-t21-evaluacion': 'Formulario T-21: Evaluación (TFEP-01/2025)',
    'formulario-t22-contenido-presentaciones-preparatorias': 'Formulario T-22: Contenido Presentaciones Preparatorias (TFEP-01/2025)',
    'formulario-e21-estructura-de-la-propuesta-economica': 'Formulario E-21: Estructura de la Propuesta Económica (TFEP-01/2025)',
    // ... (Aquí irían los títulos de Formularios E-21, E-24, E-25, E-26 si los creas) ...
  };
  // Fallback si no encuentra el título
  return titles[id] || id.split('-').map(word => word.charAt(0).toUpperCase() + word.slice(1)).join(' ');
};
</script>

<template>
  <div id="app-layout" :class="{ 'navbar-open': isNavbarOpen && isMobile }">
    <Navbar @navigate="navigateTo" :activeViewId="currentViewId" :isNavbarOpen="isNavbarOpen && isMobile" />

    <!-- Botón de hamburguesa para móviles -->
    <button class="hamburger-menu-button" @click="toggleNavbar" v-if="isMobile">
      <span class="bar top-bar" :class="{ 'open': isNavbarOpen }"></span>
      <span class="bar middle-bar" :class="{ 'open': isNavbarOpen }"></span>
      <span class="bar bottom-bar" :class="{ 'open': isNavbarOpen }"></span>
    </button>

    <main class="content-area">
      <!-- Overlay para cuando el navbar está abierto en móvil -->
      <div class="overlay" @click="toggleNavbar" v-if="isNavbarOpen && isMobile"></div>

      <!-- ==================================================================================== -->
      <!-- RENDERIZADO CONDICIONAL DE LAS VISTAS -->
      <!-- Las vistas se renderizan según el `currentViewId` -->
      <!-- ==================================================================================== -->

      <!-- Vistas del documento TFEP-01/2025 (Bases Administrativas) -->
      <Capitulo1AntecedentesYMarcoNormativoView v-if="currentViewId === 'capitulo-1-antecedentes-y-marco-normativo'" />
      <Capitulo2CondicionesGeneralesDelProcesoView
        v-else-if="currentViewId === 'capitulo-2-condiciones-generales-del-proceso'" />
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
      <Capitulo14EvaluacionAcademicaView v-else-if="currentViewId === 'capitulo-14-evaluacion-academica'" />
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

      <!-- Vistas TFEP-01/2025 (Bases Técnicas) -->
      <BtCapitulo1IntroduccionView v-else-if="currentViewId === 'bt-capitulo-1-introduccion'" />
      <BtCapitulo2AntecedentesView v-else-if="currentViewId === 'bt-capitulo-2-antecedentes'" />
      <BtCapitulo3RequerimientosGeneralesView v-else-if="currentViewId === 'bt-capitulo-3-requerimientos-generales'" />
      <BtCapitulo4InstalacionesYUsuariosView v-else-if="currentViewId === 'bt-capitulo-4-instalaciones-y-usuarios'" />
      <BtCapitulo5ProblemasActualesView v-else-if="currentViewId === 'bt-capitulo-5-problemas-actuales'" />
      <BtCapitulo6ExpectativasDeLaNuevaSolucionView
        v-else-if="currentViewId === 'bt-capitulo-6-expectativas-de-la-nueva-solucion'" />
      <BtCapitulo7InfraestructuraActualView v-else-if="currentViewId === 'bt-capitulo-7-infraestructura-actual'" />
      <BtCapitulo8RequerimientosDelProcesoView
        v-else-if="currentViewId === 'bt-capitulo-8-requerimientos-del-proceso'" />
      <BtCapitulo9RequerimientosTecnicosFuncionalesYNoFuncionalesView
        v-else-if="currentViewId === 'bt-capitulo-9-requerimientos-tecnicos-funcionales-y-no-funcionales'" />
      <BtCapitulo10RequerimientosDeLaPropuestaView
        v-else-if="currentViewId === 'bt-capitulo-10-requerimientos-de-la-propuesta'" />
      <BtCapitulo11PlanificacionView v-else-if="currentViewId === 'bt-capitulo-11-planificacion'" />
      <BtCapitulo12CaracteristicasDelSitePrincipalYSecundariosView
        v-else-if="currentViewId === 'bt-capitulo-12-caracteristicas-del-site-principal-y-secundarios'" />
      <BtCapitulo13ModeloDeOperacionMantencionYSoporteView
        v-else-if="currentViewId === 'bt-capitulo-13-modelo-de-operacion-mantencion-y-soporte'" />
      <BtCapitulo14EstructuraDelProyectoView v-else-if="currentViewId === 'bt-capitulo-14-estructura-del-proyecto'" />
      <BtCapitulo15InnovacionesView v-else-if="currentViewId === 'bt-capitulo-15-innovaciones'" />
      <BtCapitulo16InformacionCorporativaYPresenciaDigitalView
        v-else-if="currentViewId === 'bt-capitulo-16-informacion-corporativa-y-presencia-digital'" />
      <BtCapitulo17VideoDePresentacionDeLaPropuestaView
        v-else-if="currentViewId === 'bt-capitulo-17-video-de-presentacion-de-la-propuesta'" />
      <BtCapitulo18PrototipoDeInterfazYDisenoUXUIView
        v-else-if="currentViewId === 'bt-capitulo-18-prototipo-de-interfaz-y-diseno-ux-ui'" />

      <!-- Vistas TFEP-01/2025 (Anexos y Formularios) -->
      <AnexoAVolumetriaActualYProyectadaView v-else-if="currentViewId === 'anexo-a-volumetria-actual-y-proyectada'" />
      <AnexoBDefinicionesYGlosarioView v-else-if="currentViewId === 'anexo-b-definiciones-y-glosario'" />
      <FormularioA1IdentificacionDelProponenteView
        v-else-if="currentViewId === 'formulario-a1-identificacion-del-proponente'" />
      <FormularioA5IdentificacionDeDocumentosView
        v-else-if="currentViewId === 'formulario-a5-identificacion-de-documentos'" />
      <FormularioT6ExperienciaDelProponenteView
        v-else-if="currentViewId === 'formulario-t6-experiencia-del-proponente'" />
      <FormularioT7ContenidoDeLaPropuestaTecnicaView
        v-else-if="currentViewId === 'formulario-t7-contenido-de-la-propuesta-tecnica'" />
      <FormularioT9MetodologiaAdministracionYGestionView
        v-else-if="currentViewId === 'formulario-t9-metodologia-administracion-y-gestion'" />
      <FormularioT10MetodologiaDesarrolloView v-else-if="currentViewId === 'formulario-t10-metodologia-desarrollo'" />
      <FormularioT14PlanDeTrabajoEdtYCartaGanttView
        v-else-if="currentViewId === 'formulario-t14-plan-de-trabajo-edt-y-carta-gantt'" />
      <FormularioT15PlanDeTrabajosNivelacionRecursosView
        v-else-if="currentViewId === 'formulario-t15-plan-de-trabajos-nivelacion-recursos'" />
      <FormularioT16PlanDeRiesgosView v-else-if="currentViewId === 'formulario-t16-plan-de-riesgos'" />
      <FormularioT17ProtocoloDeAceptacionView v-else-if="currentViewId === 'formulario-t17-protocolo-de-aceptacion'" />
      <FormularioT18PropuestaDeImplantacionPuestaEnMarchaView
        v-else-if="currentViewId === 'formulario-t18-propuesta-de-implantacion-puesta-en-marcha'" />
      <FormularioT20CalendarioDeActividadesView
        v-else-if="currentViewId === 'formulario-t20-calendario-de-actividades'" />
      <FormularioT21EvaluacionView v-else-if="currentViewId === 'formulario-t21-evaluacion'" />
      <FormularioT22ContenidoPresentacionesPreparatoriasView
        v-else-if="currentViewId === 'formulario-t22-contenido-presentaciones-preparatorias'" />
      <FormularioE21EstructuraDeLaPropuestaEconomicaView
        v-else-if="currentViewId === 'formulario-e21-estructura-de-la-propuesta-economica'" />
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
  overflow: hidden;
  /* Evita el scroll del body al inicio y cuando el navbar está abierto */
  -webkit-overflow-scrolling: touch;
  /* Mejora el scroll en iOS */
}

body {
  font-family: 'Arial', sans-serif;
  background-color: #f0f2f5;
}

#app-layout {
  display: flex;
  height: 100vh;
  /* Asegura que el layout ocupe toda la altura del viewport */
  width: 100vw;
  position: relative;
  /* Eliminamos el transform aquí para que el contenido no se desplace con el navbar */
  /* transition: transform 0.3s ease-out; */
  /* Esto ya no es necesario aquí */
}

/* #app-layout.navbar-open ya no necesita transformar todo el layout */
/* En su lugar, haremos que el navbar se superponga */


/* Estilos por defecto para desktop */
.navbar {
  width: 280px;
  background-color: #2c3e50;
  padding: 0;
  box-shadow: 3px 0 10px rgba(0, 0, 0, 0.2);
  position: fixed;
  /* Mantiene el navbar fijo */
  top: 0;
  left: 0;
  height: 100%;
  overflow-y: auto;
  color: #ecf0f1;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  z-index: 1000;
  transform: translateX(0);
  /* Visible por defecto en desktop */
  transition: transform 0.3s ease-out;
  /* Animación de entrada/salida */
}

/* El navbar no necesita la clase is-open para desktop, siempre visible */
/* En App.vue, la prop isNavbarOpen para Navbar.vue se pasará como `isNavbarOpen && isMobile` */

.content-area {
  margin-left: 280px;
  /* Espacio para el navbar en desktop */
  flex-grow: 1;
  padding: 30px;
  box-sizing: border-box;
  overflow-y: auto;
  /* Permite scroll solo en el contenido */
  max-height: 100vh;
  /* Limita la altura del contenido al viewport */
  transition: margin-left 0.3s ease-out;
  /* Transición para el margen en resize */
}

/* Estilos del botón de hamburguesa (oculto en desktop) */
.hamburger-menu-button {
  display: none;
  /* Oculto por defecto, se mostrará en móvil */
}

/* Estilos del overlay (oculto por defecto) */
.overlay {
  display: none;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 990;
  /* Detrás del navbar, encima del contenido */
  opacity: 0;
  transition: opacity 0.3s ease-out;
}

/* Media Query para pantallas pequeñas (móviles) */
@media (max-width: 768px) {
  body {
    overflow: hidden;
    /* Asegura que el body no haga scroll cuando el navbar está abierto */
  }

  /* El content-area ya no necesita un margen en móvil, se superpondrá el navbar */
  .content-area {
    margin-left: 0;
    width: 100%;
    /* Ocupa todo el ancho */
    padding-top: 70px;
    /* Deja espacio para el botón de hamburguesa en la parte superior */
    /* Aquí permitimos el scroll si el contenido es más grande que la pantalla */
    height: 100vh;
    /* Asegura que la altura sea la del viewport */
    position: relative;
    /* Para el padding-top */
  }

  /* El navbar estará inicialmente oculto a la izquierda del viewport */
  .navbar {
    width: 280px;
    transform: translateX(-100%);
    /* Oculta el navbar a la izquierda por defecto */
    left: 0;
    /* Asegura que esté anclado a la izquierda */
    top: 0;
    position: fixed;
    /* Crucial para que se deslice por encima del contenido */
    height: 100%;
    z-index: 1010;
    /* Mayor que el overlay */
    box-shadow: 5px 0 15px rgba(0, 0, 0, 0.3);
    /* Sombra más pronunciada en móvil */
  }

  /* Cuando el navbar está abierto, lo movemos a la posición visible */
  #app-layout .navbar.is-open {
    /* Usamos #app-layout aquí para mayor especificidad */
    transform: translateX(0);
  }

  .hamburger-menu-button {
    display: flex;
    /* Muestra el botón de hamburguesa en móvil */
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
    width: 40px;
    height: 35px;
    /* Ajusta la altura para 3 barras */
    padding: 0;
    position: fixed;
    top: 20px;
    left: 20px;
    z-index: 1020;
    background-color: #007bff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
  }

  .hamburger-menu-button .bar {
    display: block;
    width: 70%;
    /* Ancho de cada barra */
    height: 3px;
    background-color: white;
    border-radius: 2px;
    transition: all 0.3s ease-in-out;
  }

  /* Animación del icono de hamburguesa a cruz */
  .hamburger-menu-button .top-bar.open {
    transform: translateY(10px) rotate(45deg);
    /* Ajusta el translateY */
  }

  .hamburger-menu-button .middle-bar.open {
    opacity: 0;
  }

  .hamburger-menu-button .bottom-bar.open {
    transform: translateY(-10px) rotate(-45deg);
    /* Ajusta el translateY */
  }

  /* Muestra el overlay y lo hace visible cuando el navbar está abierto */
  #app-layout.navbar-open .overlay {
    display: block;
    opacity: 1;
  }
}


/* Estilos del placeholder-view y main-title como están */
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