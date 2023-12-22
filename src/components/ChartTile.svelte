<script>
    import { onMount } from 'svelte';
    import axios from 'axios';
    import Chart from 'chart.js/auto';
  
    let chart = null;
    const API_URL = 'https://657ca02c853beeefdb99bbf0.mockapi.io/face_count';
  
    onMount(async () => {
      try {
        const response = await axios.get(API_URL);
        const data = response.data.sort((a, b) => new Date(a.timestamp) - new Date(b.timestamp));
        createChart(data);
      } catch (error) {
        console.error('Fehler beim Laden der Daten:', error);
      }
    });
  
    function createChart(data) {
      const ctx = document.getElementById('lineChart').getContext('2d');
      chart = new Chart(ctx, {
        type: 'line',
        data: {
          labels: data.map(item => new Date(item.timestamp).toLocaleString('de-DE', {
            day: '2-digit',
            month: '2-digit',
            year: 'numeric',
            hour: '2-digit',
            minute: '2-digit',
            second: '2-digit'
          })),
          datasets: [{
            label: 'Gemeldete Personenanzahl',
            data: data.map(item => item.faces_count),
            fill: false,
            borderColor: 'rgb(75, 192, 192)',
            tension: 0.1
          }]
        },
        options: {
          scales: {
            y: {
              beginAtZero: true
            }
          }
        }
      });
    }
  </script>

  <style>
    .chart-container {
      width: 80%;       /* Setzt die Breite des Containers auf 80% */
      margin: auto;     /* Zentriert den Container horizontal */
    }
  </style>

  <div class="chart-container">
    <canvas id="lineChart"></canvas>
  </div>