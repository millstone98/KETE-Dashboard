<script>
    import { onMount } from 'svelte';
    import axios from 'axios';
    import Chart from 'chart.js/auto';
  
    // Initialisierung der Chart-Variable, die später das Diagramm enthält.
    let chart = null;
    const API_URL = 'https://657ca02c853beeefdb99bbf0.mockapi.io/face_count';
  
    // onMount-Funktion, die beim Laden der Komponente ausgeführt wird.
    onMount(async () => {
      try {
        // Asynchroner Aufruf der API mit axios.
        const response = await axios.get(API_URL);
        // Sortieren der Daten nach dem Zeitstempel.
        const data = response.data.sort((a, b) => new Date(a.timestamp) - new Date(b.timestamp));
        // Aufruf der Funktion zur Erstellung des Diagramms mit den abgerufenen Daten.
        createChart(data);
      } catch (error) {
        console.error('Fehler beim Laden der Daten:', error);
      }
    });
  
    // Funktion zur Erstellung des Diagramms.
    function createChart(data) {
    //Erstellen der Konstante "filteredData", welche die erfassten Daten der Kamera im Linechart nur im 10-Minuten Intervall anzeigt. Zu Illustrationszwecken auskommentiert.
    /*
    const filteredData = data.reduce((acc, item) => {
        const lastItem = acc[acc.length - 1];
        const currentItemTime = new Date(item.timestamp);
        if (!lastItem || (currentItemTime - new Date(lastItem.timestamp) >= 10 * 60 * 1000)) {
            acc.push(item);
        }
        return acc;
    }, []);
    */

    // Erstellen des Liniendiagramms mit Chart.js.
    const ctx = document.getElementById('lineChart').getContext('2d');
    chart = new Chart(ctx, {
        type: 'line',
        data: {
            // Erstellen der Diagramm-Beschriftungen aus den Zeitstempeln der Daten.
            labels: data.map(item => new Date(item.timestamp).toLocaleString('de-DE', { //für 10 min Intervall hier filteredData.map statt data.map verwenden!
                day: '2-digit',
                month: '2-digit',
                year: 'numeric',
                hour: '2-digit',
                minute: '2-digit',
                second: '2-digit'
            })),
            datasets: [{
                label: 'Gemeldete Personenanzahl',
                // Setzen der Datenpunkte für das Diagramm.
                data: data.map(item => item.faces_count), //für 10 min Intervall hier filteredData.map statt data.map verwenden!
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

  <h3 style="text-align:center">Historie Personenanzahl: Liniendiagramm</h3>
  <div class="chart-container">
    <canvas id="lineChart"></canvas>
    <a href="https://657ca02c853beeefdb99bbf0.mockapi.io/face_count">Link zu Rohdaten (JSON)</a>
  </div>