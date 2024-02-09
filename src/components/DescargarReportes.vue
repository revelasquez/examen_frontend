<template>
  <div class="container">
    <h1>Descargar Reportes</h1>
    <button @click="descargarReporte()">Reporte de Préstamos por Mes</button>
    <button @click="descargarReporte2()">Reporte de Préstamos por Semana</button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  methods: {
    descargarReporte() {
      axios.get('http://localhost:8000/api/descargar-reporte-pdf-mes', { responseType: 'blob' })
        .then(response => {
          const url = window.URL.createObjectURL(new Blob([response.data]));
          const link = document.createElement('a');
          link.href = url;
          link.setAttribute('download', 'reporte.pdf');
          document.body.appendChild(link);
          link.click();
        })
        .catch(error => {
          console.error('Error al descargar el reporte:', error);
        });
    },
    descargarReporte2() {
      axios.get('http://localhost:8000/api/descargar-reporte-pdf-semana', { responseType: 'blob' })
        .then(response => {
          const url = window.URL.createObjectURL(new Blob([response.data]));
          const link = document.createElement('a');
          link.href = url;
          link.setAttribute('download', 'reporte.pdf');
          document.body.appendChild(link);
          link.click();
        })
        .catch(error => {
          console.error('Error al descargar el reporte:', error);
        });
    }
  }
}
</script>

<style>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
}

button {
  margin: 10px;
  padding: 10px 20px;
  font-size: 16px;
  border: none;
  border-radius: 5px;
  background-color: #007bff;
  color: #fff;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
</style>