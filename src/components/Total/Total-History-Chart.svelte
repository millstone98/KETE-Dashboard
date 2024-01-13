<script>
    // Importieren von 'onMount' aus der Svelte-Bibliothek und der Chart.js Bibliothek.
    import { onMount } from 'svelte';
    import Chart from 'chart.js/auto';

    // Initialisierung der Variable 'chart' zur späteren Verwendung für das Chart-Objekt.
    let chart = null;

    // Feste Daten, die im Chart angezeigt werden
    // In Praxis: durch API ersetzen
    const data = [
        { timestamp: '2023-12-21T07:00:00', faces_count: 0 },
        { timestamp: '2023-12-21T07:15:00', faces_count: 0 },
        { timestamp: '2023-12-21T07:30:00', faces_count: 0 },
        { timestamp: '2023-12-21T07:45:00', faces_count: 0 },
        { timestamp: '2023-12-21T08:00:00', faces_count: 10 },
        { timestamp: '2023-12-21T08:15:00', faces_count: 52 },
        { timestamp: '2023-12-21T08:30:00', faces_count: 104 },
        { timestamp: '2023-12-21T08:45:00', faces_count: 215 },
        { timestamp: '2023-12-21T09:00:00', faces_count: 288 },
        { timestamp: '2023-12-21T09:15:00', faces_count: 471 },
        { timestamp: '2023-12-21T09:30:00', faces_count: 488 },
        { timestamp: '2023-12-21T09:45:00', faces_count: 503 },
        { timestamp: '2023-12-21T10:00:00', faces_count: 469 },
        { timestamp: '2023-12-21T10:15:00', faces_count: 481 },
        { timestamp: '2023-12-21T10:30:00', faces_count: 512 },
        { timestamp: '2023-12-21T10:45:00', faces_count: 491 },
        { timestamp: '2023-12-21T11:00:00', faces_count: 472 },
        { timestamp: '2023-12-21T11:15:00', faces_count: 468 },
        { timestamp: '2023-12-21T11:30:00', faces_count: 410 },
        { timestamp: '2023-12-21T11:45:00', faces_count: 377 },
        { timestamp: '2023-12-21T12:00:00', faces_count: 324 },
        { timestamp: '2023-12-21T12:15:00', faces_count: 215 },
        { timestamp: '2023-12-21T12:30:00', faces_count: 105 },
        { timestamp: '2023-12-21T12:45:00', faces_count: 25 },
        { timestamp: '2023-12-21T13:00:00', faces_count: 27 },
        { timestamp: '2023-12-21T13:15:00', faces_count: 69 },
        { timestamp: '2023-12-21T13:30:00', faces_count: 255 },
        { timestamp: '2023-12-21T13:45:00', faces_count: 289 },
        { timestamp: '2023-12-21T14:00:00', faces_count: 311 },
        { timestamp: '2023-12-21T14:15:00', faces_count: 329 },
        { timestamp: '2023-12-21T14:30:00', faces_count: 347 }
    ];

  // Sobald die Komponente gemountet ist, wird das Diagramm mit den bereitgestellten Daten erstellt.
  onMount(() => {
      createChart(data);
  });

  // Funktion zum Erstellen des Liniendiagramms mit den übergebenen Daten.
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
      width: 80%;
      margin: auto;
  }
</style>

<!-- Überschrift und Container für das Diagramm -->
<h3 style="text-align:center">Historie Personenanzahl: Liniendiagramm</h3>
<div class="chart-container">
  <canvas id="lineChart"></canvas>
</div>
