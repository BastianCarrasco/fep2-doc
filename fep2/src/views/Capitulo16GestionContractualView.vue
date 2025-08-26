<script setup>
import { ref, onMounted } from 'vue';

const capituloData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/capitulo-16-gestion-contractual.json'); // Asegúrate que la ruta sea correcta
        capituloData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Capítulo 16:', error);
        errorMessage.value = 'No se pudo cargar la información del Capítulo 16.';
    }
});
</script>

<template>
    <div class="capitulo-container">
        <h1 class="main-title" v-if="capituloData">{{ capituloData.titulo_capitulo }}</h1>

        <div v-if="capituloData && capituloData.articulos" class="content">
            <div v-for="articulo in capituloData.articulos" :key="articulo.numero" class="article-block">
                <h2 class="article-title">{{ articulo.numero }}: {{ articulo.titulo }}</h2>

                <!-- ARTÍCULO 44°: ADMINISTRACIÓN DEL CONTRATO -->
                <template v-if="articulo.numero === 'ARTÍCULO 44°'">
                    <div class="sub-article-section">
                        <h3 class="subsection-title">{{ articulo.administrador_contrato.numero }} {{
                            articulo.administrador_contrato.titulo }}</h3>
                        <ul v-if="articulo.administrador_contrato.responsabilidades" class="styled-list">
                            <li v-for="(resp, index) in articulo.administrador_contrato.responsabilidades" :key="index">
                                {{ resp }}</li>
                        </ul>
                    </div>
                    <div class="sub-article-section">
                        <h3 class="subsection-title">{{ articulo.contraparte_tecnica.numero }} {{
                            articulo.contraparte_tecnica.titulo }}</h3>
                        <ul v-if="articulo.contraparte_tecnica.responsabilidades" class="styled-list">
                            <li v-for="(resp, index) in articulo.contraparte_tecnica.responsabilidades" :key="index">{{
                                resp }}</li>
                        </ul>
                    </div>
                </template>

                <!-- ARTÍCULO 45°: MODIFICACIONES CONTRACTUALES -->
                <template v-if="articulo.numero === 'ARTÍCULO 45°'">
                    <div v-for="(cond, condIndex) in articulo.condiciones" :key="condIndex" class="article-point">
                        <p><strong>{{ cond.punto }}</strong> {{ cond.descripcion }}</p>
                        <ul v-if="cond.subpuntos" class="styled-list sub-points">
                            <li v-for="(sub, subIndex) in cond.subpuntos" :key="subIndex">{{ sub }}</li>
                        </ul>
                    </div>
                </template>

                <!-- ARTÍCULO 46°: SUBCONTRATACIÓN -->
                <template v-if="articulo.numero === 'ARTÍCULO 46°'">
                    <p v-if="articulo.introduccion">{{ articulo.introduccion }}</p>
                    <p v-if="articulo.responsabilidad">{{ articulo.responsabilidad }}</p>
                </template>

            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Capítulo 16: Gestión Contractual"...</p>
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