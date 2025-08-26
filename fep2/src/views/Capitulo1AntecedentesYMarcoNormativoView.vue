<script setup>
import { ref, onMounted } from 'vue';

const capituloData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/capitulo-1-antecedentes-y-marco-normativo.json'); // Asegúrate que la ruta sea correcta
        capituloData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Capítulo 1:', error);
        errorMessage.value = 'No se pudo cargar la información del Capítulo 1.';
    }
});
</script>

<template>
    <div class="capitulo-container">
        <h1 class="main-title" v-if="capituloData">{{ capituloData.titulo_capitulo }}</h1>

        <div v-if="capituloData && capituloData.articulos" class="content">
            <div v-for="articulo in capituloData.articulos" :key="articulo.numero" class="article-block">
                <h2 class="article-title">{{ articulo.numero }}: {{ articulo.titulo }}</h2>

                <p v-if="articulo.contenido">{{ articulo.contenido }}</p>

                <!-- Artículo 3: Definiciones -->
                <template v-if="articulo.numero === 'ARTÍCULO 3°'">
                    <p v-if="articulo.introduccion">{{ articulo.introduccion }}</p>
                    <ul class="styled-list definitions-list">
                        <li v-for="definicion in articulo.definiciones" :key="definicion.numero">
                            <strong>{{ definicion.numero }} {{ definicion.termino }}:</strong> {{ definicion.definicion
                            }}
                        </li>
                    </ul>
                </template>

                <!-- Artículo 4: Marco Legal y Normativo -->
                <template v-if="articulo.numero === 'ARTÍCULO 4°'">
                    <div class="sub-article-section">
                        <h3 class="subsection-title">4.1 Rigencia de la Licitación</h3>
                        <p v-if="articulo.introduccion_rigencia">{{ articulo.introduccion_rigencia }}</p>
                        <ul class="styled-list">
                            <li v-for="(punto, index) in articulo.rigencia_puntos" :key="index">{{ punto }}</li>
                        </ul>
                    </div>
                    <div class="sub-article-section">
                        <h3 class="subsection-title">4.2 Cumplimiento Normativo de Participantes</h3>
                        <p v-if="articulo.cumplimiento_participantes">{{ articulo.cumplimiento_participantes }}</p>
                        <ul class="styled-list">
                            <li v-for="(norma, index) in articulo.normativa_puntos" :key="index">{{ norma }}</li>
                        </ul>
                    </div>
                </template>

                <!-- Artículo 5: Documentos que rigen la Licitación -->
                <template v-if="articulo.numero === 'ARTÍCULO 5°'">
                    <div class="sub-article-section">
                        <h3 class="subsection-title">5.1 Orden de Precedencia</h3>
                        <p v-if="articulo.orden_precedencia_introduccion">{{ articulo.orden_precedencia_introduccion }}
                        </p>
                        <ul class="styled-list ordered-list">
                            <li v-for="(doc, index) in articulo.orden_precedencia" :key="index">{{ doc }}</li>
                        </ul>
                    </div>
                    <p v-if="articulo.integracion_documentos">{{ articulo.integracion_documentos }}</p>
                    <p v-if="articulo.discrepancia_documentos">{{ articulo.discrepancia_documentos }}</p>
                </template>

            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Capítulo 1: Antecedentes y Marco Normativo"...</p>
    </div>
</template>

<style scoped>
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

.article-block {
    margin-bottom: 40px;
    border-left: 4px solid #0056b3;
    /* Un color ligeramente diferente al principal para destacar los artículos */
    padding-left: 20px;
}

.article-title {
    color: #0056b3;
    /* Título de artículo */
    margin-top: 35px;
    margin-bottom: 15px;
    font-size: 1.9em;
    font-weight: bold;
}

.sub-article-section {
    margin-top: 25px;
    margin-bottom: 25px;
    border-left: 2px solid #e0e0e0;
    /* Una línea más delgada para sub-secciones dentro de artículos */
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
    /* Quitamos el estilo de disco predeterminado para mayor control */
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

/* Bullet personalizado para listas */
.styled-list li::before {
    content: '•';
    position: absolute;
    left: 0;
    color: #007bff;
    /* Color del bullet */
    font-size: 1em;
    top: 0;
}

/* Para listas ordenadas específicas (como el Artículo 5.1) */
.styled-list.ordered-list li::before {
    content: '';
    /* Quitamos el bullet para permitir la numeración que viene en el texto */
}


.definitions-list li {
    margin-bottom: 12px;
    padding-left: 0;
    /* Sin padding-left extra para que el número 3.1 quede al inicio */
}

.definitions-list li strong {
    color: #007bff;
    /* Color para el número y el término en definiciones */
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