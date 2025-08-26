<script setup>
import { ref, onMounted } from 'vue';

const capituloData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/capitulo-9-recepcion-y-apertura-de-ofertas.json'); // Asegúrate que la ruta sea correcta
        capituloData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Capítulo 9:', error);
        errorMessage.value = 'No se pudo cargar la información del Capítulo 9.';
    }
});
</script>

<template>
    <div class="capitulo-container">
        <h1 class="main-title" v-if="capituloData">{{ capituloData.titulo_capitulo }}</h1>

        <div v-if="capituloData && capituloData.articulos" class="content">
            <div v-for="articulo in capituloData.articulos" :key="articulo.numero" class="article-block">
                <h2 class="article-title">{{ articulo.numero }}: {{ articulo.titulo }}</h2>

                <!-- ARTÍCULO 24°: PRESENTACIÓN DE OFERTAS -->
                <template v-if="articulo.numero === 'ARTÍCULO 24°'">
                    <p v-if="articulo.introduccion">{{ articulo.introduccion }}</p>
                    <ul v-if="articulo.sobres_presentacion" class="styled-list">
                        <li v-for="(sobre, index) in articulo.sobres_presentacion" :key="index">{{ sobre }}</li>
                    </ul>
                    <p v-if="articulo.condicion_plazo" class="important-note">{{ articulo.condicion_plazo }}</p>
                </template>

                <!-- ARTÍCULO 25°: SOBRE N° 1 - ANTECEDENTES ADMINISTRATIVOS -->
                <template v-if="articulo.numero === 'ARTÍCULO 25°'">
                    <h3 class="subsection-title">{{ articulo.caratula_fisico.titulo }}</h3>
                    <div class="caratula-box">
                        <p v-for="(linea, index) in articulo.caratula_fisico.contenido" :key="index">{{ linea }}</p>
                    </div>
                    <h3 class="subsection-title">{{ articulo.contenido_sobre.titulo }}</h3>
                    <ul v-if="articulo.contenido_sobre.puntos" class="styled-list">
                        <li v-for="(punto, index) in articulo.contenido_sobre.puntos" :key="index">{{ punto }}</li>
                    </ul>
                    <h3 class="subsection-title">{{ articulo.formato_digital.titulo }}</h3>
                    <ul v-if="articulo.formato_digital.puntos" class="styled-list">
                        <li v-for="(punto, index) in articulo.formato_digital.puntos" :key="index">{{ punto }}</li>
                    </ul>
                </template>

                <!-- ARTÍCULO 26°: SOBRE N° 2 - OFERTA TÉCNICA -->
                <template v-if="articulo.numero === 'ARTÍCULO 26°'">
                    <p v-if="articulo.contenido_obligatorio">{{ articulo.contenido_obligatorio }}</p>
                    <p v-if="articulo.restriccion">{{ articulo.restriccion }}</p>
                    <h3 class="subsection-title">{{ articulo.formato_digital.titulo }}</h3>
                    <ul v-if="articulo.formato_digital.puntos" class="styled-list">
                        <li v-for="(punto, index) in articulo.formato_digital.puntos" :key="index">{{ punto }}</li>
                    </ul>
                </template>

                <!-- ARTÍCULO 27°: SOBRE N° 3 - OFERTA ECONÓMICA -->
                <template v-if="articulo.numero === 'ARTÍCULO 27°'">
                    <p v-if="articulo.contenido_obligatorio">{{ articulo.contenido_obligatorio }}</p>
                    <h3 class="subsection-title">{{ articulo.formato_presentacion.titulo }}</h3>
                    <ul v-if="articulo.formato_presentacion.puntos" class="styled-list">
                        <li v-for="(punto, index) in articulo.formato_presentacion.puntos" :key="index">{{ punto }}</li>
                    </ul>
                    <h3 class="subsection-title">{{ articulo.formato_digital.titulo }}</h3>
                    <ul v-if="articulo.formato_digital.puntos" class="styled-list">
                        <li v-for="(punto, index) in articulo.formato_digital.puntos" :key="index">{{ punto }}</li>
                    </ul>
                </template>

                <!-- ARTÍCULO 28°: ACTO DE APERTURA -->
                <template v-if="articulo.numero === 'ARTÍCULO 28°'">
                    <h3 class="subsection-title">{{ articulo.apertura_sobre_1.titulo }}</h3>
                    <ul v-if="articulo.apertura_sobre_1.puntos" class="styled-list">
                        <li v-for="(punto, index) in articulo.apertura_sobre_1.puntos" :key="index">{{ punto }}</li>
                    </ul>
                    <h3 class="subsection-title">{{ articulo.custodia.titulo }}</h3>
                    <ul v-if="articulo.custodia.puntos" class="styled-list">
                        <li v-for="(punto, index) in articulo.custodia.puntos" :key="index">{{ punto }}</li>
                    </ul>
                </template>

            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Capítulo 9: Recepción y Apertura de Ofertas"...</p>
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

.article-block {
    margin-bottom: 40px;
    border-left: 4px solid #0056b3;
    padding-left: 20px;
}

.article-title {
    color: #0056b3;
    margin-top: 35px;
    margin-bottom: 15px;
    font-size: 1.9em;
    font-weight: bold;
}

p {
    margin-bottom: 10px;
    text-align: justify;
}

strong {
    color: #222;
}

.subsection-title {
    color: #4a4a4a;
    margin-top: 20px;
    margin-bottom: 10px;
    font-size: 1.5em;
    font-weight: 600;
}

.caratula-box {
    border: 1px dashed #ccc;
    padding: 15px;
    margin-left: 20px;
    margin-bottom: 20px;
    background-color: #f9f9f9;
}

.caratula-box p {
    margin: 5px 0;
    text-align: left;
}

.important-note {
    font-weight: bold;
    color: #d9534f;
    /* Un color de advertencia */
    margin-top: 20px;
    margin-bottom: 20px;
    padding: 10px 15px;
    border: 1px solid #d9534f;
    border-radius: 5px;
    background-color: #fdf7f7;
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