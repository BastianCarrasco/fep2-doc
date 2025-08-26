<script setup>
import { ref, onMounted } from 'vue';

const capituloData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/bt-capitulo-16-informacion-corporativa-y-presencia-digital.json'); // Asegúrate que la ruta sea correcta
        capituloData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Capítulo 16 (Bases Técnicas):', error);
        errorMessage.value = 'No se pudo cargar la información del Capítulo 16 (Bases Técnicas).';
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

                    <!-- Requisitos Obligatorios (16.1.1) -->
                    <template v-if="subsection.numero === '16.1.1'">
                        <div v-if="subsection.informacion_institucional">
                            <h4 class="sub-subsection-title">{{ subsection.informacion_institucional.titulo }}</h4>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.informacion_institucional.puntos" :key="index">
                                    {{ punto }}</li>
                            </ul>
                        </div>
                        <div v-if="subsection.experiencia_casos_exito">
                            <h4 class="sub-subsection-title">{{ subsection.experiencia_casos_exito.titulo }}</h4>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.experiencia_casos_exito.puntos" :key="index">{{
                                    punto }}</li>
                            </ul>
                        </div>
                        <div v-if="subsection.equipo_profesional">
                            <h4 class="sub-subsection-title">{{ subsection.equipo_profesional.titulo }}</h4>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.equipo_profesional.puntos" :key="index">{{ punto
                                    }}</li>
                            </ul>
                        </div>
                        <div v-if="subsection.capacidades_tecnicas">
                            <h4 class="sub-subsection-title">{{ subsection.capacidades_tecnicas.titulo }}</h4>
                            <ul class="styled-list">
                                <li v-for="(punto, index) in subsection.capacidades_tecnicas.puntos" :key="index">{{
                                    punto }}</li>
                            </ul>
                        </div>
                    </template>

                    <!-- Información Adicional Valorada (16.1.2) -->
                    <template v-if="subsection.numero === '16.1.2'">
                        <ul v-if="subsection.puntos_valorados" class="styled-list">
                            <li v-for="(punto, index) in subsection.puntos_valorados" :key="index">{{ punto }}</li>
                        </ul>
                    </template>
                </div>

                <!-- Causales de Descalificación (16.2) o Declaración de Veracidad (16.3) -->
                <template v-if="seccion.causales_descalificacion">
                    <h3 class="subsection-title">{{ seccion.causales_descalificacion.titulo }}</h3>
                    <ul class="styled-list">
                        <li v-for="(punto, index) in seccion.causales_descalificacion.puntos" :key="index">{{ punto }}
                        </li>
                    </ul>
                </template>
                <template v-if="seccion.puntos_declaracion">
                    <h3 class="subsection-title">{{ seccion.introduccion }}</h3>
                    <ul class="styled-list">
                        <li v-for="(punto, index) in seccion.puntos_declaracion" :key="index">{{ punto }}</li>
                    </ul>
                </template>

            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Capítulo 16: Información Corporativa y Presencia Digital (Bases
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

.sub-subsection-title {
    color: #5d5d5d;
    margin-top: 18px;
    margin-bottom: 8px;
    font-size: 1.3em;
    font-weight: 500;
    border-bottom: 1px dashed #eee;
    padding-bottom: 5px;
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