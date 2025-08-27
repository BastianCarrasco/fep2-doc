<script setup>
import { ref, onMounted } from 'vue';

const formData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textosbases/formulario-a1-identificacion-del-proponente.json'); // Asegúrate que la ruta sea correcta
        formData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el Formulario A-1:', error);
        errorMessage.value = 'No se pudo cargar la información del Formulario A-1.';
    }
});
</script>

<template>
    <div class="formulario-container">
        <h1 class="main-title" v-if="formData">{{ formData.titulo_formulario }}</h1>
        <h2 class="sub-title" v-if="formData">{{ formData.subtitulo }}</h2>

        <div v-if="formData && formData.secciones" class="content">
            <div v-for="seccion in formData.secciones" :key="seccion.numero" class="section-block">
                <h3 class="subsection-title">{{ seccion.numero }} {{ seccion.titulo }}</h3>
                <div v-for="(campo, index) in seccion.campos" :key="index" class="form-field">
                    <template v-if="campo.tipo === 'header'">
                        <p class="field-header">{{ campo.etiqueta }}</p>
                    </template>
                    <template v-else-if="campo.opciones">
                        <p class="field-label">{{ campo.numero }} {{ campo.nombre }}</p>
                        <div class="options-group">
                            <span v-for="(opcion, optIndex) in campo.opciones" :key="optIndex" class="form-option">
                                {{ opcion.letra }}) {{ opcion.descripcion }}
                            </span>
                        </div>
                    </template>
                    <template v-else>
                        <label class="field-label">{{ campo.numero || campo.letra }}) {{ campo.nombre }}:</label>
                        <span class="field-value">{{ campo.valor_ejemplo }}</span>
                    </template>
                </div>
            </div>

            <div v-if="formData.firma" class="firma-section">
                <p class="firma-line">{{ formData.firma.texto }}</p>
                <p class="firma-label">{{ formData.firma.cargo }}</p>
                <p class="firma-date">{{ formData.firma.lugar_fecha }}</p>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Formulario A-1"...</p>
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

.section-block {
    margin-bottom: 30px;
    border-left: 3px solid #e0e0e0;
    padding-left: 15px;
}

.subsection-title {
    color: #4a4a4a;
    margin-top: 20px;
    margin-bottom: 15px;
    font-size: 1.4em;
    font-weight: bold;
}

.form-field {
    margin-bottom: 15px;
}

.field-header {
    font-weight: bold;
    font-size: 1.1em;
    margin-bottom: 10px;
    color: #333;
}

.field-label {
    font-weight: 500;
    color: #555;
    margin-right: 5px;
    display: inline;
}

.field-value {
    color: #777;
    font-style: italic;
}

.options-group {
    margin-top: 5px;
    margin-left: 20px;
}

.form-option {
    display: inline-block;
    margin-right: 20px;
    color: #666;
}

.firma-section {
    margin-top: 50px;
    text-align: right;
    border-top: 1px solid #eee;
    padding-top: 20px;
}

.firma-line {
    margin: 0;
    font-size: 1.1em;
    font-weight: bold;
    color: #333;
}

.firma-label {
    margin: 5px 0 0 0;
    font-size: 0.9em;
    color: #555;
}

.firma-date {
    margin: 5px 0 0 0;
    font-size: 0.9em;
    color: #555;
    font-style: italic;
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