<script setup>
import { ref, onMounted } from 'vue';

const capituloData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/bt-capitulo-8-requerimientos-del-proceso.json'); // Asegúrate que la ruta sea correcta
        capituloData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Capítulo 8 (Bases Técnicas):', error);
        errorMessage.value = 'No se pudo cargar la información del Capítulo 8 (Bases Técnicas).';
    }
});
</script>

<template>
    <div class="capitulo-container">
        <h1 class="main-title" v-if="capituloData">{{ capituloData.titulo_capitulo }}</h1>

        <div v-if="capituloData && capituloData.secciones_principales" class="content">
            <div v-for="seccion in capituloData.secciones_principales" :key="seccion.numero" class="section-block">
                <h2 class="section-title">{{ seccion.numero }} {{ seccion.titulo }}</h2>

                <!-- Renderiza la introducción si existe (para 8.2) -->
                <p v-if="seccion.introduccion">{{ seccion.introduccion }}</p>

                <!-- Si la sección tiene puntos directos (ej. 8.3 Ciclo de Orden de Compra, 8.5 Portal y Aplicación Móvil) -->
                <ul v-if="seccion.puntos && !seccion.funcionalidades_comprador && !seccion.modalidades"
                    class="styled-list">
                    <li v-for="(punto, index) in seccion.puntos" :key="index">{{ punto }}</li>
                </ul>

                <!-- Para secciones con modalidades (ej. 8.2 Gestión de Cotizaciones) -->
                <ul v-if="seccion.modalidades" class="styled-list">
                    <li v-for="(modalidad, index) in seccion.modalidades" :key="index">{{ modalidad }}</li>
                </ul>

                <!-- Para todas las sub-estructuras con títulos y listas de puntos -->
                <!-- Simplificamos la condición del v-if envolvente -->
                <template
                    v-if="seccion.funcionalidades_comprador || seccion.funcionalidades_proveedor || seccion.gestion || seccion.administracion || seccion.portal_ciudadano || seccion.portal_proveedores_no_registrados || seccion.tipos_garantias || seccion.funcionalidades || seccion.ciclo_vida || seccion.funcionalidades_adicionales || seccion.proceso_reclamos || seccion.proceso_impugnaciones || seccion.sistema_evaluacion || seccion.indicadores || seccion.control_presupuestario || seccion.para_compradores || seccion.integracion_compras || seccion.dashboards_ejecutivos || seccion.analisis_avanzado || seccion.integraciones_requeridas || seccion.metodos_integracion || seccion.repositorio_centralizado || seccion.canales_comunicacion || seccion.elearning_integrado || seccion.trazabilidad_completa || seccion.funcionalidades_marketplace || seccion.para_servicios_continuos || seccion.aplicaciones_nativas || seccion.compras_verdes || seccion.portal_innovacion || seccion.sistema_gestion_riesgos || seccion.estandares_internacionales || seccion.proceso_registro /* <-- ¡Añadido aquí! */">
                    <div class="sub-section-group">
                        <template v-if="seccion.funcionalidades_comprador">
                            <h3 class="subsection-title">{{ seccion.funcionalidades_comprador.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.funcionalidades_comprador.puntos" :key="index">{{
                                    punto }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.funcionalidades_proveedor">
                            <h3 class="subsection-title">{{ seccion.funcionalidades_proveedor.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.funcionalidades_proveedor.puntos" :key="index">{{
                                    punto }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.gestion">
                            <h3 class="subsection-title">{{ seccion.gestion.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.gestion.puntos" :key="index">{{ punto }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.administracion">
                            <h3 class="subsection-title">{{ seccion.administracion.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.administracion.puntos" :key="index">{{ punto }}
                                </li>
                            </ul>
                        </template>
                        <template v-if="seccion.portal_ciudadano">
                            <h3 class="subsection-title">{{ seccion.portal_ciudadano.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.portal_ciudadano.puntos" :key="index">{{ punto }}
                                </li>
                            </ul>
                        </template>
                        <template v-if="seccion.portal_proveedores_no_registrados">
                            <h3 class="subsection-title">{{ seccion.portal_proveedores_no_registrados.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.portal_proveedores_no_registrados.puntos"
                                    :key="index">{{ punto }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.tipos_garantias">
                            <h3 class="subsection-title">{{ seccion.tipos_garantias.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.tipos_garantias.puntos" :key="index">{{ punto }}
                                </li>
                            </ul>
                        </template>
                        <template v-if="seccion.funcionalidades && seccion.numero === '8.10'">
                            <h3 class="subsection-title">{{ seccion.funcionalidades.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.funcionalidades.puntos" :key="index">{{ punto }}
                                </li>
                            </ul>
                        </template>
                        <template v-if="seccion.ciclo_vida">
                            <h3 class="subsection-title">{{ seccion.ciclo_vida.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.ciclo_vida.puntos" :key="index">{{ punto }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.funcionalidades_adicionales">
                            <h3 class="subsection-title">{{ seccion.funcionalidades_adicionales.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.funcionalidades_adicionales.puntos" :key="index">{{
                                    punto }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.proceso_reclamos">
                            <h3 class="subsection-title">{{ seccion.proceso_reclamos.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.proceso_reclamos.puntos" :key="index">{{ punto }}
                                </li>
                            </ul>
                        </template>
                        <template v-if="seccion.proceso_impugnaciones">
                            <h3 class="subsection-title">{{ seccion.proceso_impugnaciones.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.proceso_impugnaciones.puntos" :key="index">{{ punto
                                }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.sistema_evaluacion">
                            <h3 class="subsection-title">{{ seccion.sistema_evaluacion.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.sistema_evaluacion.puntos" :key="index">{{ punto }}
                                </li>
                            </ul>
                        </template>
                        <template v-if="seccion.indicadores">
                            <h3 class="subsection-title">{{ seccion.indicadores.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.indicadores.puntos" :key="index">{{ punto }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.control_presupuestario">
                            <h3 class="subsection-title">{{ seccion.control_presupuestario.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.control_presupuestario.puntos" :key="index">{{
                                    punto }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.para_compradores">
                            <h3 class="subsection-title">{{ seccion.para_compradores.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.para_compradores.puntos" :key="index">{{ punto }}
                                </li>
                            </ul>
                        </template>
                        <template v-if="seccion.integracion_compras">
                            <h3 class="subsection-title">{{ seccion.integracion_compras.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.integracion_compras.puntos" :key="index">{{ punto
                                }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.dashboards_ejecutivos">
                            <h3 class="subsection-title">{{ seccion.dashboards_ejecutivos.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.dashboards_ejecutivos.puntos" :key="index">{{ punto
                                }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.analisis_avanzado">
                            <h3 class="subsection-title">{{ seccion.analisis_avanzado.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.analisis_avanzado.puntos" :key="index">{{ punto }}
                                </li>
                            </ul>
                        </template>
                        <template v-if="seccion.integraciones_requeridas">
                            <h3 class="subsection-title">{{ seccion.integraciones_requeridas.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.integraciones_requeridas.puntos" :key="index">{{
                                    punto }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.metodos_integracion">
                            <h3 class="subsection-title">{{ seccion.metodos_integracion.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.metodos_integracion.puntos" :key="index">{{ punto
                                }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.repositorio_centralizado">
                            <h3 class="subsection-title">{{ seccion.repositorio_centralizado.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.repositorio_centralizado.puntos" :key="index">{{
                                    punto }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.canales_comunicacion">
                            <h3 class="subsection-title">{{ seccion.canales_comunicacion.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.canales_comunicacion.puntos" :key="index">{{ punto
                                }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.elearning_integrado">
                            <h3 class="subsection-title">{{ seccion.elearning_integrado.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.elearning_integrado.puntos" :key="index">{{ punto
                                }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.trazabilidad_completa">
                            <h3 class="subsection-title">{{ seccion.trazabilidad_completa.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.trazabilidad_completa.puntos" :key="index">{{ punto
                                }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.funcionalidades_marketplace">
                            <h3 class="subsection-title">{{ seccion.funcionalidades_marketplace.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.funcionalidades_marketplace.puntos" :key="index">{{
                                    punto }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.para_servicios_continuos">
                            <h3 class="subsection-title">{{ seccion.para_servicios_continuos.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.para_servicios_continuos.puntos" :key="index">{{
                                    punto }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.aplicaciones_nativas">
                            <h3 class="subsection-title">{{ seccion.aplicaciones_nativas.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.aplicaciones_nativas.puntos" :key="index">{{ punto
                                }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.compras_verdes">
                            <h3 class="subsection-title">{{ seccion.compras_verdes.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.compras_verdes.puntos" :key="index">{{ punto }}
                                </li>
                            </ul>
                        </template>
                        <template v-if="seccion.portal_innovacion">
                            <h3 class="subsection-title">{{ seccion.portal_innovacion.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.portal_innovacion.puntos" :key="index">{{ punto }}
                                </li>
                            </ul>
                        </template>
                        <template v-if="seccion.sistema_gestion_riesgos">
                            <h3 class="subsection-title">{{ seccion.sistema_gestion_riesgos.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.sistema_gestion_riesgos.puntos" :key="index">{{
                                    punto }}</li>
                            </ul>
                        </template>
                        <template v-if="seccion.estandares_internacionales">
                            <h3 class="subsection-title">{{ seccion.estandares_internacionales.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.estandares_internacionales.puntos" :key="index">{{
                                    punto }}</li>
                            </ul>
                        </template>
                        <!-- AÑADIDO: Renderizado para `proceso_registro` -->
                        <template v-if="seccion.proceso_registro">
                            <h3 class="subsection-title">{{ seccion.proceso_registro.titulo }}</h3>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in seccion.proceso_registro.puntos" :key="index">{{ punto }}
                                </li>
                            </ul>
                        </template>
                    </div>
                </template>

            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Capítulo 8: Requerimientos del Proceso (Bases Técnicas)"...</p>
    </div>
</template>

<style scoped>
/* Estilos generales del Capítulo */
.capitulo-container {
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

.section-block {
    margin-bottom: 45px;
    border-left: 4px solid #0056b3;
    padding-left: 20px;
}

.section-title {
    color: #0056b3;
    margin-top: 35px;
    margin-bottom: 15px;
    font-size: 1.9em;
    font-weight: bold;
}

.sub-section-group {
    margin-top: 25px;
    margin-bottom: 25px;
    border-left: 2px solid #e0e0e0;
    padding-left: 15px;
}

.subsection-title {
    color: #4a4a4a;
    margin-top: 20px;
    margin-bottom: 10px;
    font-size: 1.5em;
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

.styled-list li::before {
    content: '•';
    position: absolute;
    left: 0;
    color: #007bff;
    font-size: 1em;
    top: 0;
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