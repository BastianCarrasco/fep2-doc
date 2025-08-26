<script setup>
import { ref, onMounted } from 'vue';

const capituloData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/capitulo-13-evaluacion-final-y-adjudicacion.json'); // Asegúrate que la ruta sea correcta
        capituloData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Capítulo 13:', error);
        errorMessage.value = 'No se pudo cargar la información del Capítulo 13.';
    }
});
</script>

<template>
    <div class="capitulo-container">
        <h1 class="main-title" v-if="capituloData">{{ capituloData.titulo_capitulo }}</h1>

        <div v-if="capituloData && capituloData.articulos" class="content">
            <div v-for="articulo in capituloData.articulos" :key="articulo.numero" class="article-block">
                <h2 class="article-title">{{ articulo.numero }}: {{ articulo.titulo }}</h2>

                <!-- ARTÍCULO 37°: PUNTAJE FINAL -->
                <template v-if="articulo.numero === 'ARTÍCULO 37°'">
                    <p v-if="articulo.formula_introduccion">{{ articulo.formula_introduccion }}</p>
                    <p class="formula-display">{{ articulo.formula_contenido }}</p>
                    <p v-if="articulo.ponderaciones_introduccion" class="subsection-intro">{{
                        articulo.ponderaciones_introduccion }}</p>
                    <ul v-if="articulo.ponderaciones_detalle" class="styled-list">
                        <li v-for="(ponderacion, index) in articulo.ponderaciones_detalle" :key="index">{{ ponderacion
                            }}</li>
                    </ul>
                </template>

                <!-- ARTÍCULO 38°: CRITERIOS DE ADJUDICACIÓN -->
                <template v-if="articulo.numero === 'ARTÍCULO 38°'">
                    <p v-if="articulo.criterio_principal">{{ articulo.criterio_principal }}</p>
                    <p v-if="articulo.empate_introduccion" class="subsection-intro">{{ articulo.empate_introduccion }}
                    </p>
                    <ul v-if="articulo.criterios_empate" class="styled-list sub-points">
                        <li v-for="(criterio, index) in articulo.criterios_empate" :key="index">{{ criterio }}</li>
                    </ul>
                    <p v-if="articulo.derecho_cliente_introduccion" class="subsection-intro">{{
                        articulo.derecho_cliente_introduccion }}</p>
                    <ul v-if="articulo.derechos_cliente" class="styled-list">
                        <li v-for="(derecho, index) in articulo.derechos_cliente" :key="index">{{ derecho }}</li>
                    </ul>
                </template>

                <!-- ARTÍCULO 39°: NOTIFICACIÓN Y PUBLICACIÓN -->
                <template v-if="articulo.numero === 'ARTÍCULO 39°'">
                    <p v-if="articulo.notificacion_introduccion">{{ articulo.notificacion_introduccion }}</p>
                    <ul v-if="articulo.forma_notificacion" class="styled-list">
                        <li v-for="(forma, index) in articulo.forma_notificacion" :key="index">{{ forma }}</li>
                    </ul>
                    <p v-if="articulo.plazo_notificacion">{{ articulo.plazo_notificacion }}</p>
                </template>

            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Capítulo 13: Evaluación Final y Adjudicación"...</p>
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

.subsection-intro {
    font-weight: 500;
    color: #666;
    margin-top: 10px;
    margin-bottom: 5px;
    padding-left: 5px;
}

.formula-display {
    font-family: 'Consolas', 'Courier New', monospace;
    background-color: #f0f0f0;
    padding: 10px 15px;
    border-left: 4px solid #007bff;
    margin: 20px 0;
    overflow-x: auto;
    font-size: 1.1em;
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