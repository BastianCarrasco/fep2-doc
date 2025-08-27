<script setup>
import { ref, onMounted } from 'vue';

const formData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/formulario-t7-contenido-de-la-propuesta-tecnica.json'); // Asegúrate que la ruta sea correcta
        formData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Formulario T-7:', error);
        errorMessage.value = 'No se pudo cargar la información del Formulario T-7.';
    }
});
</script>

<template>
    <div class="formulario-container">
        <h1 class="main-title" v-if="formData">{{ formData.titulo_formulario }}</h1>
        <h2 class="sub-title" v-if="formData">{{ formData.subtitulo }}</h2>

        <div v-if="formData" class="content">
            <p v-for="(inst, index) in formData.instrucciones_generales" :key="index" class="form-instruction">
                {{ inst }}</p>

            <h3 class="subsection-title">{{ formData.tabla_contenido.titulo }}</h3>

            <div v-for="(subdoc, docIndex) in formData.tabla_contenido.subdocumentos" :key="docIndex"
                class="subdocument-block">
                <h4 class="subdocument-title">{{ subdoc.titulo_subdocumento }}</h4>

                <div v-for="(seccion, secIndex) in subdoc.secciones" :key="secIndex" class="section-content-block">
                    <h5 class="section-content-title">{{ seccion.numero }} {{ seccion.titulo }}</h5>
                    <p v-if="seccion.contenido">{{ seccion.contenido }}</p>

                    <!-- Subsecciones con letras (a, b, c...) -->
                    <template
                        v-if="seccion.subsecciones_alcance || seccion.subsecciones_logica || seccion.subsecciones_fisica || seccion.subsecciones_ventajas || seccion.subsecciones_metodologias || seccion.subsecciones_plan_trabajo || seccion.subsecciones_operacion || seccion.subsecciones_planes_operacion">
                        <div v-for="(sub, subsubIndex) in (seccion.subsecciones_alcance || seccion.subsecciones_logica || seccion.subsecciones_fisica || seccion.subsecciones_ventajas || seccion.subsecciones_metodologias || seccion.subsecciones_plan_trabajo || seccion.subsecciones_operacion || seccion.subsecciones_planes_operacion)"
                            :key="subsubIndex" class="sub-section-content">
                            <p><strong>{{ sub.letra }}</strong> {{ sub.titulo }}: {{ sub.contenido }}</p>
                        </div>
                    </template>
                </div>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Formulario T-7"...</p>
    </div>
</template>

<style scoped>
.formulario-container {
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
    margin-bottom: 5px;
    font-size: 2em;
    font-weight: bold;
    text-align: center;
}

.sub-title {
    color: #007bff;
    margin-bottom: 30px;
    border-bottom: 2px solid #007bff;
    padding-bottom: 10px;
    font-size: 1.5em;
    font-weight: 600;
    text-align: center;
}

.form-instruction {
    font-style: italic;
    color: #555;
    margin-bottom: 10px;
    text-align: justify;
}

.subsection-title {
    color: #4a4a4a;
    margin-top: 25px;
    margin-bottom: 15px;
    font-size: 1.6em;
    font-weight: bold;
    border-bottom: 1px dashed #eee;
    padding-bottom: 5px;
}

.subdocument-block {
    margin-top: 30px;
    margin-bottom: 30px;
    border-left: 3px solid #ccc;
    padding-left: 15px;
}

.subdocument-title {
    color: #0056b3;
    margin-top: 20px;
    margin-bottom: 10px;
    font-size: 1.4em;
    font-weight: 600;
}

.section-content-block {
    margin-top: 15px;
    margin-bottom: 15px;
    padding-left: 10px;
}

.section-content-title {
    color: #333;
    margin-top: 10px;
    margin-bottom: 5px;
    font-size: 1.2em;
    font-weight: bold;
}

.sub-section-content p {
    margin-bottom: 5px;
    text-align: justify;
    padding-left: 10px;
    /* Indentación para a), b) */
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