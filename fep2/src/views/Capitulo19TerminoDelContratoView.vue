<script setup>
import { ref, onMounted } from 'vue';

const capituloData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/capitulo-19-termino-del-contrato.json'); // Asegúrate que la ruta sea correcta
        capituloData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Capítulo 19:', error);
        errorMessage.value = 'No se pudo cargar la información del Capítulo 19.';
    }
});
</script>

<template>
    <div class="capitulo-container">
        <h1 class="main-title" v-if="capituloData">{{ capituloData.titulo_capitulo }}</h1>

        <div v-if="capituloData && capituloData.articulos" class="content">
            <div v-for="articulo in capituloData.articulos" :key="articulo.numero" class="article-block">
                <h2 class="article-title">{{ articulo.numero }}: {{ articulo.titulo }}</h2>

                <!-- ARTÍCULO 52°: CAUSALES DE TÉRMINO -->
                <template v-if="articulo.numero === 'ARTÍCULO 52°'">
                    <p v-if="articulo.introduccion">{{ articulo.introduccion }}</p>
                    <div v-for="(causal, causalIndex) in articulo.causales" :key="causalIndex" class="article-point">
                        <p><strong>{{ causal.numero }}</strong> {{ causal.descripcion }}</p>
                        <ul v-if="causal.subpuntos" class="styled-list sub-points">
                            <li v-for="(sub, subIndex) in causal.subpuntos" :key="subIndex">{{ sub }}</li>
                        </ul>
                    </div>
                </template>

                <!-- ARTÍCULO 53°: PROCEDIMIENTO DE TÉRMINO -->
                <template v-if="articulo.numero === 'ARTÍCULO 53°'">
                    <p v-if="articulo.introduccion">{{ articulo.introduccion }}</p>
                    <ul v-if="articulo.procedimientos" class="styled-list ordered-list">
                        <li v-for="(proc, index) in articulo.procedimientos" :key="index">{{ proc }}</li>
                    </ul>
                </template>

            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Capítulo 19: Término del Contrato"...</p>
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

.article-point {
    margin-bottom: 15px;
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
    content: '-';
    color: #4a4a4a;
}

.styled-list.ordered-list li {
    padding-left: 0;
    /* Si el número ya viene en el texto */
}

.styled-list.ordered-list li::before {
    content: '';
    /* Ocultar bullet si el número viene en el texto */
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