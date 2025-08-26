<script setup>
import { ref, onMounted } from 'vue';

const capituloData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/capitulo-7-consultas-y-aclaraciones.json'); // Asegúrate que la ruta sea correcta
        capituloData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Capítulo 7:', error);
        errorMessage.value = 'No se pudo cargar la información del Capítulo 7.';
    }
});
</script>

<template>
    <div class="capitulo-container">
        <h1 class="main-title" v-if="capituloData">{{ capituloData.titulo_capitulo }}</h1>

        <div v-if="capituloData && capituloData.articulos" class="content">
            <div v-for="articulo in capituloData.articulos" :key="articulo.numero" class="article-block">
                <h2 class="article-title">{{ articulo.numero }}: {{ articulo.titulo }}</h2>

                <!-- ARTÍCULO 20°: PERÍODO DE CONSULTAS -->
                <template v-if="articulo.numero === 'ARTÍCULO 20°'">
                    <p v-if="articulo.introduccion_periodo">{{ articulo.introduccion_periodo }}</p>
                    <p v-if="articulo.formato_consultas" class="subsection-intro">{{ articulo.formato_consultas }}</p>
                    <ul v-if="articulo.columnas_excel" class="styled-list sub-points">
                        <li v-for="(col, index) in articulo.columnas_excel" :key="index">{{ col }}</li>
                    </ul>
                    <p v-if="articulo.nombre_archivo" class="subsection-intro">{{ articulo.nombre_archivo }}</p>
                    <p v-if="articulo.ejemplo_archivo" class="code-example">{{ articulo.ejemplo_archivo }}</p>
                    <p v-if="articulo.cliente_respondera" class="subsection-intro">{{ articulo.cliente_respondera }}</p>
                    <ul v-if="articulo.criterios_respuesta" class="styled-list sub-points">
                        <li v-for="(criterio, index) in articulo.criterios_respuesta" :key="index">{{ criterio }}</li>
                    </ul>
                </template>

                <!-- ARTÍCULO 21°: ACLARACIONES Y MODIFICACIONES -->
                <template v-if="articulo.numero === 'ARTÍCULO 21°'">
                    <p v-if="articulo.introduccion_aclaraciones">{{ articulo.introduccion_aclaraciones }}</p>
                    <p v-if="articulo.notificacion_modificaciones">{{ articulo.notificacion_modificaciones }}</p>
                </template>

            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Capítulo 7: Consultas y Aclaraciones"...</p>
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

.subsection-intro {
    font-weight: bold;
    margin-top: 15px;
    margin-bottom: 5px;
}

.code-example {
    font-family: 'Courier New', monospace;
    background-color: #f0f0f0;
    padding: 8px 12px;
    border-radius: 4px;
    margin-left: 20px;
    display: inline-block;
    /* Para que no ocupe todo el ancho si no es necesario */
    white-space: pre-wrap;
    /* Mantiene saltos de línea y espacios */
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
    content: '-';
    /* Usa un guion para los subpuntos */
    color: #4a4a4a;
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