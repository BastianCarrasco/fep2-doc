<script setup>
import { ref, onMounted } from 'vue';

const capituloData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/bt-capitulo-18-prototipo-de-interfaz-y-diseno-ux-ui.json'); // Asegúrate que la ruta sea correcta
        capituloData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Capítulo 18 (Bases Técnicas):', error);
        errorMessage.value = 'No se pudo cargar la información del Capítulo 18 (Bases Técnicas).';
    }
});
</script>

<template>
    <div class="capitulo-container">
        <h1 class="main-title" v-if="capituloData">{{ capituloData.titulo_capitulo }}</h1>

        <div v-if="capituloData && capituloData.secciones_principales" class="content">
            <div v-for="seccion in capituloData.secciones_principales" :key="seccion.numero" class="section-block">
                <h2 class="section-title">{{ seccion.numero }} {{ seccion.titulo }}</h2>

                <div v-for="subsection in seccion.subsecciones" :key="subsection.numero" class="sub-section-group">
                    <h3 class="subsection-title">{{ subsection.numero }} {{ subsection.titulo }}</h3>
                    <p v-if="subsection.introduccion">{{ subsection.introduccion }}</p>
                    <p v-if="subsection.simulacion_realista">{{ subsection.simulacion_realista }}</p>

                    <!-- Portal Principal (18.1.2) -->
                    <template v-if="subsection.portal_principal">
                        <h4 class="sub-subsection-title">{{ subsection.portal_principal.titulo }}</h4>
                        <ul class="styled-list">
                            <li v-for="(punto, index) in subsection.portal_principal.puntos" :key="index">{{ punto }}
                            </li>
                        </ul>
                    </template>
                    <!-- Módulos Obligatorios (18.1.2) -->
                    <template v-if="subsection.modulos_obligatorios_a_prototipar">
                        <h4 class="sub-subsection-title">{{ subsection.modulos_obligatorios_a_prototipar.titulo }}</h4>
                        <div v-for="modulo in subsection.modulos_obligatorios_a_prototipar.puntos" :key="modulo.numero"
                            class="module-block">
                            <h5>{{ modulo.numero }} {{ modulo.titulo }}</h5>
                            <ul v-if="modulo.subpuntos" class="styled-list sub-points">
                                <li v-for="(subpunto, index) in modulo.subpuntos" :key="index">{{ subpunto }}</li>
                            </ul>
                        </div>
                    </template>

                    <!-- Principios de Diseño UX/UI (18.1.3) -->
                    <template v-if="subsection.principios_de_diseno">
                        <h4 class="sub-subsection-title">{{ subsection.principios_de_diseno.introduccion }}</h4>
                        <div v-if="subsection.principios_de_diseno.usabilidad">
                            <h6>{{ subsection.principios_de_diseno.usabilidad.titulo }}</h6>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.principios_de_diseno.usabilidad.puntos"
                                    :key="index">{{ punto }}</li>
                            </ul>
                        </div>
                        <div v-if="subsection.principios_de_diseno.accesibilidad">
                            <h6>{{ subsection.principios_de_diseno.accesibilidad.titulo }}</h6>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.principios_de_diseno.accesibilidad.puntos"
                                    :key="index">{{ punto }}</li>
                            </ul>
                        </div>
                        <div v-if="subsection.principios_de_diseno.diseno_responsivo">
                            <h6>{{ subsection.principios_de_diseno.diseno_responsivo.titulo }}</h6>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.principios_de_diseno.diseno_responsivo.puntos"
                                    :key="index">{{ punto }}</li>
                            </ul>
                        </div>
                        <div v-if="subsection.principios_de_diseno.consistencia_visual">
                            <h6>{{ subsection.principios_de_diseno.consistencia_visual.titulo }}</h6>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.principios_de_diseno.consistencia_visual.puntos"
                                    :key="index">{{ punto }}</li>
                            </ul>
                        </div>
                    </template>

                    <!-- Elementos de Interfaz Requeridos (18.1.4) -->
                    <template v-if="subsection.componentes_obligatorios">
                        <h4 class="sub-subsection-title">{{ subsection.componentes_obligatorios.introduccion }}</h4>
                        <div v-if="subsection.componentes_obligatorios.navegacion">
                            <h6>{{ subsection.componentes_obligatorios.navegacion.titulo }}</h6>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.componentes_obligatorios.navegacion.puntos"
                                    :key="index">{{ punto }}</li>
                            </ul>
                        </div>
                        <div v-if="subsection.componentes_obligatorios.formularios">
                            <h6>{{ subsection.componentes_obligatorios.formularios.titulo }}</h6>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.componentes_obligatorios.formularios.puntos"
                                    :key="index">{{ punto }}</li>
                            </ul>
                        </div>
                        <div v-if="subsection.componentes_obligatorios.visualizacion_datos">
                            <h6>{{ subsection.componentes_obligatorios.visualizacion_datos.titulo }}</h6>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.componentes_obligatorios.visualizacion_datos.puntos"
                                    :key="index">{{ punto }}</li>
                            </ul>
                        </div>
                        <div v-if="subsection.componentes_obligatorios.retroalimentacion">
                            <h6>{{ subsection.componentes_obligatorios.retroalimentacion.titulo }}</h6>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.componentes_obligatorios.retroalimentacion.puntos"
                                    :key="index">{{ punto }}</li>
                            </ul>
                        </div>
                        <div v-if="subsection.componentes_obligatorios.elementos_accion">
                            <h6>{{ subsection.componentes_obligatorios.elementos_accion.titulo }}</h6>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.componentes_obligatorios.elementos_accion.puntos"
                                    :key="index">{{ punto }}</li>
                            </ul>
                        </div>
                    </template>

                    <!-- Requerimientos de Entrega (18.1.5) -->
                    <template v-if="subsection.requerimientos_entrega">
                        <h4 class="sub-subsection-title">{{ subsection.requerimientos_entrega.titulo }}</h4>
                        <ul class="styled-list">
                            <li v-for="(punto, index) in subsection.requerimientos_entrega.puntos" :key="index">{{ punto
                            }}</li>
                        </ul>
                    </template>
                    <!-- Nivel de Interactividad (18.1.5) -->
                    <template v-if="subsection.nivel_interactividad">
                        <h4 class="sub-subsection-title">{{ subsection.nivel_interactividad.titulo }}</h4>
                        <ul class="styled-list">
                            <li v-for="(punto, index) in subsection.nivel_interactividad.puntos" :key="index">{{ punto
                            }}</li>
                        </ul>
                    </template>

                    <!-- Documentación del Diseño (18.1.6) -->
                    <template v-if="subsection.arquitectura_informacion">
                        <h4 class="sub-subsection-title">{{ subsection.arquitectura_informacion.titulo }}</h4>
                        <ul class="styled-list">
                            <li v-for="(punto, index) in subsection.arquitectura_informacion.puntos" :key="index">{{
                                punto }}</li>
                        </ul>
                    </template>

                    <!-- No se Requiere (18.1.7) -->
                    <template v-if="subsection.no_se_requiere">
                        <h4 class="sub-subsection-title">{{ subsection.no_se_requiere.titulo }}</h4>
                        <ul class="styled-list">
                            <li v-for="(punto, index) in subsection.no_se_requiere.puntos" :key="index">{{ punto }}</li>
                        </ul>
                    </template>
                    <!-- Se Penalizará (18.1.7) -->
                    <template v-if="subsection.se_penalizara">
                        <h4 class="sub-subsection-title">{{ subsection.se_penalizara.titulo }}</h4>
                        <ul class="styled-list">
                            <li v-for="(punto, index) in subsection.se_penalizara.puntos" :key="index">{{ punto }}</li>
                        </ul>
                    </template>

                    <!-- Propiedad Intelectual (18.1.8) -->
                    <template v-if="subsection.derechos_y_licencias">
                        <h4 class="sub-subsection-title">{{ subsection.derechos_y_licencias.titulo }}</h4>
                        <ul class="styled-list">
                            <li v-for="(punto, index) in subsection.derechos_y_licencias.puntos" :key="index">{{ punto
                            }}</li>
                        </ul>
                    </template>

                </div>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Capítulo 18: Prototipo de Interfaz y Diseño UX/UI (Bases
            Técnicas)"...</p>
    </div>
</template>

<style scoped>
/* Estilos para h6 */
h6 {
    /* Cambié `.h6` a `h6` directamente */
    font-size: 1.2em;
    /* Aumentado de 1.1em que estaba por defecto para module-block h5 */
    font-weight: bold;
    margin-top: 20px;
    margin-bottom: 10px;
    color: #333;
    border-bottom: 1px dotted #ccc;
    /* Añadido un borde inferior sutil */
    padding-bottom: 5px;
    margin-left: 5px;
    /* Ligeramente indentado */
}

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

.sub-subsection-title {
    color: #5d5d5d;
    margin-top: 18px;
    margin-bottom: 8px;
    font-size: 1.3em;
    font-weight: 500;
    border-bottom: 1px dashed #eee;
    padding-bottom: 5px;
}

.module-block {
    margin-top: 10px;
    margin-left: 10px;
    padding-left: 10px;
    border-left: 1px dotted #ccc;
}

.module-block h5 {
    color: #6a737d;
    font-size: 1.1em;
    /* Mantener h5 más pequeño si h6 es el "título" de grupo */
    margin-bottom: 5px;
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

.styled-list.sub-points li::before {
    content: '';
    position: static;
    margin-right: 5px;
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