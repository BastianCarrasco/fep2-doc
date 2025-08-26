<script setup>
import { ref, onMounted } from 'vue';

const preambuloData = ref(null);
const errorMessage = ref('');

onMounted(async () => {
    try {
        const response = await import('../textos/preambulo.json');
        preambuloData.value = response.default;
    } catch (error) {
        console.error('Error al cargar el preámbulo:', error);
        errorMessage.value = 'No se pudo cargar la información del preámbulo.';
    }
});
</script>

<template>
    <div class="preambulo-container">
        <h1 class="main-title" v-if="preambuloData">{{ preambuloData.titulo }}</h1>

        <div v-if="preambuloData && preambuloData.preambulo" class="preambulo-content">
            <h2 class="section-title">Preámbulo</h2>

            <div class="section-block">
                <h3 class="subsection-title">Organismo Nacional</h3>
                <p><strong>Nombre:</strong> {{ preambuloData.preambulo.organismo_nacional.nombre }}</p>
                <p><strong>Rol:</strong> {{ preambuloData.preambulo.organismo_nacional.rol }}</p>
                <p><strong>Afiliaciones:</strong></p>
                <ul class="styled-list">
                    <li v-for="afiliacion in preambuloData.preambulo.organismo_nacional.afiliaciones" :key="afiliacion">
                        {{ afiliacion }}
                    </li>
                </ul>
                <p><strong>Representación ante:</strong> {{
                    preambuloData.preambulo.organismo_nacional.representacion_ante }}</p>
            </div>

            <div class="section-block">
                <h3 class="subsection-title">Preparación de la Norma</h3>
                <p><strong>Nombre de la Norma:</strong> {{ preambuloData.preambulo.preparacion_norma.nombre_norma }}</p>
                <p><strong>Preparado por:</strong> {{ preambuloData.preambulo.preparacion_norma.preparado_por }}</p>
                <p><strong>Participantes:</strong></p>
                <ul class="styled-list">
                    <li v-for="(participante, index) in preambuloData.preambulo.preparacion_norma.participantes"
                        :key="index">
                        {{ participante.organismo }}:
                        <span v-if="participante.persona">{{ participante.persona }}</span>
                        <span v-else-if="participante.personas">{{ participante.personas.join(', ') }}</span>
                    </li>
                </ul>
            </div>

            <div class="section-block">
                <h3 class="subsection-title">Objetivo de la Norma</h3>
                <p>{{ preambuloData.preambulo.objetivo_norma }}</p>
            </div>

            <div class="section-block">
                <h3 class="subsection-title">Homologación Internacional</h3>
                <p><strong>Norma Original:</strong> {{ preambuloData.preambulo.homologacion_internacional.norma_original
                    }}</p>
                <p><strong>Identidad con Original:</strong> {{
                    preambuloData.preambulo.homologacion_internacional.identidad_con_original }}</p>
                <p><strong>Acuerdos del Comité Técnico INN:</strong></p>
                <ul class="styled-list">
                    <li v-for="(acuerdo, index) in preambuloData.preambulo.homologacion_internacional.acuerdos_comite_tecnico_inn"
                        :key="index">
                        {{ acuerdo }}
                    </li>
                </ul>
            </div>

            <div class="section-block">
                <h3 class="subsection-title">Términos Técnicos</h3>
                <div class="table-responsive">
                    <table>
                        <thead>
                            <tr>
                                <th>Término en inglés (ISO/IEC 17799: 2000)</th>
                                <th>Término utilizado en la norma chilena</th>
                                <th>Otros términos de uso habitual en el país</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(termino, index) in preambuloData.preambulo.homologacion_internacional.terminos_tecnicos"
                                :key="index">
                                <td>{{ termino.ingles_iso_iec_17799_2000 }}</td>
                                <td>{{ termino.termino_norma_chilena }}</td>
                                <td>{{ termino.otros_terminos_uso_habitual_pais || 'N/A' }}</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <div class="section-block">
                <h3 class="subsection-title">Aprobación y Oficialización</h3>
                <p><strong>Aprobado por:</strong> {{ preambuloData.preambulo.aprobacion_oficializacion.aprobado_por }}
                </p>
                <p><strong>Fecha de Aprobación:</strong> {{
                    preambuloData.preambulo.aprobacion_oficializacion.fecha_aprobacion }}</p>
                <p><strong>Declarada Oficial por:</strong> {{
                    preambuloData.preambulo.aprobacion_oficializacion.declarada_oficial_por }}</p>
                <p><strong>Fecha de Resolución:</strong> {{
                    preambuloData.preambulo.aprobacion_oficializacion.fecha_resolucion }}</p>
                <p><strong>Publicada en:</strong> {{ preambuloData.preambulo.aprobacion_oficializacion.publicada_en }}
                </p>
            </div>
        </div>

        <p v-else-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        <p v-else class="loading-message">Cargando preámbulo...</p>
    </div>
</template>

<style scoped>
.preambulo-container {
    padding: 30px;
    /* Aumenta el padding general */
    background-color: #ffffff;
    /* Fondo blanco para el contenido */
    border-radius: 8px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
    /* Sombra más suave */
    line-height: 1.6;
    /* Mayor espaciado entre líneas */
    color: #333;
    /* Color de texto base */
    font-family: Georgia, serif;
    /* Fuente más clásica para documentos */
}

.main-title {
    color: #1a237e;
    /* Azul oscuro distintivo para el título principal */
    margin-bottom: 30px;
    border-bottom: 2px solid #007bff;
    /* Línea de acento debajo del título */
    padding-bottom: 15px;
    font-size: 2.2em;
    /* Título principal más grande */
    font-weight: bold;
    text-align: center;
}

.section-title {
    color: #007bff;
    /* Azul primario para títulos de sección */
    margin-top: 40px;
    margin-bottom: 20px;
    font-size: 1.8em;
    font-weight: bold;
    position: relative;
    padding-left: 15px;
}

.section-title::before {
    content: '▪';
    /* Punto decorativo */
    position: absolute;
    left: 0;
    color: #007bff;
    font-size: 1.2em;
    top: 50%;
    transform: translateY(-50%);
}

.section-block {
    margin-bottom: 30px;
    /* Espacio entre bloques de contenido */
    border-left: 3px solid #e0e0e0;
    /* Barra lateral para agrupar */
    padding-left: 15px;
}

.subsection-title {
    color: #4a4a4a;
    margin-top: 25px;
    margin-bottom: 10px;
    font-size: 1.4em;
    font-weight: 600;
}

p {
    margin-bottom: 10px;
}

strong {
    color: #222;
    /* Hace el texto fuerte un poco más oscuro */
}

.styled-list {
    list-style: disc;
    /* Puntos tradicionales */
    margin-left: 25px;
    /* Indentación para las listas */
    margin-bottom: 15px;
    padding-left: 0;
}

.styled-list li {
    margin-bottom: 8px;
    line-height: 1.5;
    color: #555;
}

.table-responsive {
    overflow-x: auto;
    /* Permite desplazamiento horizontal en tablas grandes */
    margin-top: 20px;
    margin-bottom: 30px;
}

table {
    width: 100%;
    border-collapse: collapse;
    min-width: 600px;
    /* Asegura que la tabla no se haga demasiado pequeña */
}

th,
td {
    border: 1px solid #e0e0e0;
    /* Bordes más suaves */
    padding: 12px 15px;
    text-align: left;
    vertical-align: top;
    font-size: 0.9em;
}

th {
    background-color: #f5f7fa;
    /* Fondo más claro para los encabezados */
    font-weight: 700;
    color: #333;
    text-transform: uppercase;
}

tbody tr:nth-child(even) {
    background-color: #fcfdff;
    /* Rayas ligeras para la tabla */
}

tbody tr:hover {
    background-color: #eef7ff;
    /* Resalta la fila al pasar el mouse */
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