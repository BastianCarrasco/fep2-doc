<script setup>
import { ref, onMounted } from 'vue';

const politicaData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textos/seguridad.json'); // Asegúrate que el nombre del archivo JSON coincida aquí
        politicaData.value = response.default;
    } catch (error) {
        console.error('Error al cargar la sección "Política de seguridad":', error);
        errorMessage.value = 'No se pudo cargar la información de "Política de seguridad".';
    }
});
</script>

<template>
    <div class="politica-container">
        <h1 class="main-title" v-if="politicaData">{{ politicaData.titulo_seccion }}</h1>

        <div v-if="politicaData && politicaData.secciones" class="politica-content">
            <div v-for="section in politicaData.secciones" :key="section.numero" class="section-block">
                <h2 class="section-title">{{ section.numero }} {{ section.titulo }}</h2>
                <p v-if="section.objetivo">{{ section.objetivo }}</p>

                <div v-for="subsection in section.subsecciones" :key="subsection.numero" class="subsection-block">
                    <h3 class="subsection-title">{{ subsection.numero }} {{ subsection.titulo }}</h3>
                    <p v-if="subsection.parrafo_introductorio">{{ subsection.parrafo_introductorio }}</p>

                    <ul v-if="subsection.puntos_guia" class="styled-list">
                        <li v-for="(punto, index) in subsection.puntos_guia" :key="index">
                            <strong>{{ punto.letra }}</strong> {{ punto.descripcion }}
                            <ul v-if="punto.subpuntos" class="sub-styled-list">
                                <li v-for="(subpunto, subIndex) in punto.subpuntos" :key="subIndex">
                                    {{ subpunto }}
                                </li>
                            </ul>
                        </li>
                    </ul>

                    <p v-if="subsection.comunicacion">{{ subsection.comunicacion }}</p>

                    <ul v-if="subsection.puntos_revision" class="styled-list">
                        <li v-for="(punto, index) in subsection.puntos_revision" :key="index">
                            <strong>{{ punto.letra }}</strong> {{ punto.descripcion }}
                        </li>
                    </ul>
                </div>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando "Política de seguridad"...</p>
    </div>
</template>

<style scoped>
/* Copia y pega los estilos generales de tus otras vistas aquí */
/* Asegúrate de cambiar la clase principal del contenedor si la cambiaste en el template */

.politica-container {
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

.section-title {
    color: #007bff;
    margin-top: 40px;
    margin-bottom: 20px;
    font-size: 1.8em;
    font-weight: bold;
    position: relative;
    padding-left: 15px;
}

.section-title::before {
    content: '▪';
    position: absolute;
    left: 0;
    color: #007bff;
    font-size: 1.2em;
    top: 50%;
    transform: translateY(-50%);
}

.section-block {
    margin-bottom: 30px;
    border-left: 3px solid #e0e0e0;
    padding-left: 15px;
}

.subsection-block {
    margin-top: 25px;
    margin-bottom: 20px;
}

.subsection-title {
    color: #4a4a4a;
    margin-top: 20px;
    margin-bottom: 10px;
    font-size: 1.4em;
    font-weight: 600;
}

p {
    margin-bottom: 10px;
}

strong {
    color: #222;
}

.styled-list {
    list-style: none;
    /* Quitamos el estilo de disco predeterminado */
    margin-left: 0;
    margin-bottom: 15px;
    padding-left: 20px;
    /* Indentación para la lista principal */
}

.styled-list li {
    margin-bottom: 8px;
    line-height: 1.5;
    color: #555;
    position: relative;
}

.styled-list li strong {
    margin-right: 5px;
    /* Espacio entre la letra (a), (b), etc. y el texto */
}

/* Bullet para la lista principal (a, b, c...) */
.styled-list li::before {
    content: attr(data-letter);
    /* Usa el atributo data-letter si lo tuvieras, sino un bullet fijo */
    position: absolute;
    left: 0;
    color: #007bff;
    font-size: 1em;
    top: 0;
    font-weight: bold;
}

/* Como el JSON ya incluye la letra en el texto, podemos simplemente usar un bullet por defecto o quitar ::before */
.styled-list li::before {
    content: '';
    /* Quita el bullet personalizado ya que la letra está en el strong */
    position: static;
    /* Restablece la posición */
}


.sub-styled-list {
    list-style: disc;
    /* Vuelve a usar disco para las sublistas (c.1, c.2) */
    margin-left: 25px;
    /* Indenta la sublista */
    margin-top: 5px;
    margin-bottom: 5px;
}

.sub-styled-list li {
    margin-bottom: 5px;
    line-height: 1.4;
    color: #666;
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