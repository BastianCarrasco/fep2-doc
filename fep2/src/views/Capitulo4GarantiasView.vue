<script setup>
import { ref, onMounted } from 'vue';

const capituloData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/capitulo-4-garantias.json'); // Asegúrate que la ruta sea correcta
        capituloData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Capítulo 4:', error);
        errorMessage.value = 'No se pudo cargar la información del Capítulo 4.';
    }
});
</script>

<template>
    <div class="capitulo-container">
        <h1 class="main-title" v-if="capituloData">{{ capituloData.titulo_capitulo }}</h1>

        <div v-if="capituloData && capituloData.articulos" class="content">
            <div v-for="articulo in capituloData.articulos" :key="articulo.numero" class="article-block">
                <h2 class="article-title">{{ articulo.numero }}: {{ articulo.titulo }}</h2>

                <!-- ARTÍCULO 14°: GARANTÍA DE SERIEDAD DE LA OFERTA -->
                <template v-if="articulo.numero === 'ARTÍCULO 14°'">
                    <p v-if="articulo.introduccion_garantia">{{ articulo.introduccion_garantia }}</p>
                    <p class="strong-text">{{ articulo.ejecucion_boleta }}</p>
                    <ul v-if="articulo.casos_ejecucion" class="styled-list">
                        <li v-for="(caso, index) in articulo.casos_ejecucion" :key="index">{{ caso }}</li>
                    </ul>
                    <p v-if="articulo.devolucion_garantia">{{ articulo.devolucion_garantia }}</p>
                    <p v-if="articulo.presentacion_requisito">{{ articulo.presentacion_requisito }}</p>
                </template>

                <!-- ARTÍCULO 15°: GARANTÍA DE FIEL CUMPLIMIENTO DEL CONTRATO -->
                <template v-if="articulo.numero === 'ARTÍCULO 15°'">
                    <p v-if="articulo.introduccion_garantia">{{ articulo.introduccion_garantia }}</p>
                    <ul v-if="articulo.instrucciones_garantia" class="styled-list">
                        <li v-for="(inst, index) in articulo.instrucciones_garantia" :key="index">{{ inst }}</li>
                    </ul>
                    <p v-if="articulo.entrega_reemplazo">{{ articulo.entrega_reemplazo }}</p>
                </template>

            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Capítulo 4: Garantías"...</p>
    </div>
</template>

<style scoped>
/* Copia y pega los estilos generales del Capítulo 1 aquí, puedes añadir clases específicas si necesitas */
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

.strong-text {
    font-weight: bold;
    margin-top: 15px;
    margin-bottom: 10px;
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