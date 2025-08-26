<script setup>
import { ref, onMounted } from 'vue';

const capituloData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/bt-capitulo-3-requerimientos-generales.json'); // Asegúrate que la ruta sea correcta
        capituloData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Capítulo 3 (Bases Técnicas):', error);
        errorMessage.value = 'No se pudo cargar la información del Capítulo 3 (Bases Técnicas).';
    }
});
</script>

<template>
    <div class="capitulo-container">
        <h1 class="main-title" v-if="capituloData">{{ capituloData.titulo_capitulo }}</h1>

        <div v-if="capituloData && capituloData.secciones_principales" class="content">
            <div v-for="seccion in capituloData.secciones_principales" :key="seccion.numero" class="section-block">
                <h2 class="section-title">{{ seccion.numero }} {{ seccion.titulo }}</h2>

                <template v-if="seccion.subsecciones">
                    <div v-for="(sub, subIndex) in seccion.subsecciones" :key="subIndex" class="sub-section-group">
                        <h3 class="subsection-title" v-if="sub.titulo_subseccion">{{ sub.titulo_subseccion }}</h3>

                        <!-- Lógica mejorada para manejar `sub.contenido` o `sub.puntos` directamente -->
                        <template v-if="sub.contenido">
                            <!-- Para estructuras como "Primera Etapa", "Segunda Etapa" -->
                            <div v-for="(etapa, etapaIndex) in sub.contenido" :key="etapaIndex">
                                <p v-if="etapa.titulo" class="sub-section-intro"><strong>{{ etapa.titulo }}</strong></p>
                                <ul v-if="etapa.puntos" class="styled-list">
                                    <li v-for="(punto, puntoIndex) in etapa.puntos" :key="puntoIndex">{{ punto }}</li>
                                </ul>
                            </div>
                        </template>
                        <template v-else-if="sub.puntos">
                            <!-- Para estructuras como "Infraestructura Mixta:" -->
                            <ul class="styled-list">
                                <li v-for="(punto, puntoIndex) in sub.puntos" :key="puntoIndex">{{ punto }}</li>
                            </ul>
                        </template>
                    </div>
                </template>
                <ul v-else-if="seccion.puntos" class="styled-list">
                    <li v-for="(punto, index) in seccion.puntos" :key="index">{{ punto }}</li>
                </ul>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Capítulo 3: Requerimientos Generales (Bases Técnicas)"...</p>
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

.sub-section-intro {
    font-weight: bold;
    margin-bottom: 8px;
    margin-top: 15px;
    color: #333;
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