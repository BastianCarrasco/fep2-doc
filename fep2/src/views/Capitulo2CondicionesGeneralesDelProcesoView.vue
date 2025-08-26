<script setup>
import { ref, onMounted } from 'vue';

const capituloData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/capitulo-2-condiciones-generales-del-proceso.json'); // Asegúrate que la ruta sea correcta
        capituloData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Capítulo 2:', error);
        errorMessage.value = 'No se pudo cargar la información del Capítulo 2.';
    }
});
</script>

<template>
    <div class="capitulo-container">
        <h1 class="main-title" v-if="capituloData">{{ capituloData.titulo_capitulo }}</h1>

        <div v-if="capituloData && capituloData.articulos" class="content">
            <div v-for="articulo in capituloData.articulos" :key="articulo.numero" class="article-block">
                <h2 class="article-title">{{ articulo.numero }}: {{ articulo.titulo }}</h2>

                <!-- Contenido general de los artículos con estructura de puntos numerados -->
                <template v-if="articulo.contenido && Array.isArray(articulo.contenido)">
                    <div v-for="(item, index) in articulo.contenido" :key="index" class="article-point">
                        <p><strong>{{ item.punto }}</strong> {{ item.descripcion }}</p>
                        <ul v-if="item.subpuntos" class="styled-list sub-points">
                            <li v-for="(sub, subIndex) in item.subpuntos" :key="subIndex">{{ sub }}</li>
                        </ul>
                    </div>
                </template>

                <!-- Artículo 8: Moneda y Valores -->
                <template v-if="articulo.numero === 'ARTÍCULO 8°'">
                    <div class="sub-article-section">
                        <p v-if="articulo.moneda_introduccion">{{ articulo.moneda_introduccion }}</p>
                        <ul class="styled-list">
                            <li v-for="(moneda, index) in articulo.monedas" :key="index">{{ moneda }}</li>
                        </ul>
                    </div>
                    <div class="sub-article-section">
                        <p v-if="articulo.valores_introduccion">{{ articulo.valores_introduccion }}</p>
                        <ul class="styled-list">
                            <li v-for="(valor, index) in articulo.valores_detalle" :key="index">{{ valor }}</li>
                        </ul>
                    </div>
                    <p v-if="articulo.evaluacion_cambio">{{ articulo.evaluacion_cambio }}</p>
                </template>

                <!-- Artículo 10: Gastos del Proceso -->
                <template v-if="articulo.numero === 'ARTÍCULO 10°'">
                    <p v-if="articulo.introduccion_gastos">{{ articulo.introduccion_gastos }}</p>
                    <p v-if="articulo.reembolsos">{{ articulo.reembolsos }}</p>
                    <div class="sub-article-section">
                        <p v-if="articulo.incluye_gastos">{{ articulo.incluye_gastos }}</p>
                        <ul class="styled-list">
                            <li v-for="(gasto, index) in articulo.gastos_detalle" :key="index">{{ gasto }}</li>
                        </ul>
                    </div>
                </template>

            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Capítulo 2: Condiciones Generales del Proceso"...</p>
    </div>
</template>

<style scoped>
/* Copia y pega los estilos generales del Capítulo 1 aquí, con pequeños ajustes si es necesario */
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

.article-point {
    margin-bottom: 15px;
    /* Espacio entre los puntos 1., 2., 3. de cada artículo */
}

.sub-article-section {
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
    /* Espacio para el bullet personalizado si se usa */
}

/* Bullet personalizado para listas */
.styled-list li::before {
    content: '•';
    position: absolute;
    left: 0;
    color: #007bff;
    font-size: 1em;
    top: 0;
}

/* Para sub-puntos (como los de Moneda y Valores) que usan el bullet por defecto */
.styled-list.sub-points li::before {
    content: '';
    /* Quita el bullet personalizado para los subpuntos */
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