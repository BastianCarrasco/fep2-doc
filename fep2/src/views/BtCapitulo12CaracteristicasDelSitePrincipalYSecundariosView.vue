<script setup>
import { ref, onMounted } from 'vue';

const capituloData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/bt-capitulo-12-caracteristicas-del-site-principal-y-secundarios.json'); // Asegúrate que la ruta sea correcta
        capituloData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Capítulo 12 (Bases Técnicas):', error);
        errorMessage.value = 'No se pudo cargar la información del Capítulo 12 (Bases Técnicas).';
    }
});
</script>

<template>
    <div class="capitulo-container">
        <h1 class="main-title" v-if="capituloData">{{ capituloData.titulo_capitulo }}</h1>

        <div v-if="capituloData" class="content">
            <p v-if="capituloData.introduccion_general">{{ capituloData.introduccion_general }}</p>
            <ul v-if="capituloData.caracteristicas_generales" class="styled-list">
                <li v-for="(caract, index) in capituloData.caracteristicas_generales" :key="index">{{ caract }}</li>
            </ul>

            <p v-if="capituloData.parrafo_personal_operacion">{{ capituloData.parrafo_personal_operacion }}</p>
            <p v-if="capituloData.distribucion_base_site_primario">{{ capituloData.distribucion_base_site_primario }}
            </p>

            <div v-for="seccion in capituloData.subsecciones" :key="seccion.numero" class="section-block">
                <h2 class="section-title">{{ seccion.numero.split('_')[0] }} {{ seccion.titulo }}</h2>

                <!-- 12.1 Site Principal (Interno) -->
                <template v-if="seccion.numero === '12.1'">
                    <h3 class="subsection-title" v-if="seccion.especificaciones_datacenter">{{
                        seccion.especificaciones_datacenter.titulo }}</h3>
                    <ul v-if="seccion.especificaciones_datacenter && seccion.especificaciones_datacenter.puntos"
                        class="styled-list">
                        <li v-for="(punto, index) in seccion.especificaciones_datacenter.puntos" :key="index">{{ punto
                            }}</li>
                    </ul>
                </template>

                <!-- 12.2 Site Secundario (Nube) -->
                <template v-if="seccion.numero === '12.2'">
                    <ul v-if="seccion.puntos" class="styled-list">
                        <li v-for="(punto, index) in seccion.puntos" :key="index">{{ punto }}</li>
                    </ul>
                </template>

                <!-- 12.3 SLA Requeridos -->
                <template v-if="seccion.numero === '12.3_sla'">
                    <template v-if="seccion.infraestructura">
                        <h3 class="subsection-title">{{ seccion.infraestructura.titulo }}</h3>
                        <ul class="styled-list">
                            <li v-for="(punto, index) in seccion.infraestructura.puntos" :key="index">{{ punto }}</li>
                        </ul>
                    </template>
                    <template v-if="seccion.aplicaciones">
                        <h3 class="subsection-title">{{ seccion.aplicaciones.titulo }}</h3>
                        <ul class="styled-list">
                            <li v-for="(punto, index) in seccion.aplicaciones.puntos" :key="index">{{ punto }}</li>
                        </ul>
                    </template>
                </template>

                <!-- 12.3 Implementación de Espacio Físico -->
                <template v-if="seccion.numero === '12.3_implementacion'">
                    <p v-if="seccion.introduccion">{{ seccion.introduccion }}</p>
                    <ul v-if="seccion.consideraciones_fuera_site" class="styled-list">
                        <li v-for="(cons, index) in seccion.consideraciones_fuera_site" :key="index">{{ cons }}</li>
                    </ul>
                    <p v-if="seccion.proveedor_adjudicado_obligacion">{{ seccion.proveedor_adjudicado_obligacion }}</p>
                    <p v-if="seccion.habilitacion_site_secundario">{{ seccion.habilitacion_site_secundario }}</p>
                </template>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Capítulo 12: Características del Site Principal y Secundarios (Bases
            Técnicas)"...</p>
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