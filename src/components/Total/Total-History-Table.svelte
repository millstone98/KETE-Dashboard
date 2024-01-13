<script>
  import { onMount } from 'svelte';

  // Feste Daten, die in der Tabelle angezeigt werden
  // In Praxis: durch API ersetzen
  let data = [
    { timestamp: '2023-12-21T14:15:00', faces_count: 347 },
    { timestamp: '2023-12-21T14:00:00', faces_count: 311 },
    { timestamp: '2023-12-21T13:45:00', faces_count: 289 },
    { timestamp: '2023-12-21T13:30:00', faces_count: 255 },
    { timestamp: '2023-12-21T13:15:00', faces_count: 69 },
    { timestamp: '2023-12-21T13:00:00', faces_count: 27 },
    { timestamp: '2023-12-21T12:45:00', faces_count: 25 },
    { timestamp: '2023-12-21T12:30:00', faces_count: 105 },
    { timestamp: '2023-12-21T12:15:00', faces_count: 215 },
    { timestamp: '2023-12-21T12:00:00', faces_count: 324 },
    { timestamp: '2023-12-21T11:45:00', faces_count: 377 },
    { timestamp: '2023-12-21T11:30:00', faces_count: 410 },
    { timestamp: '2023-12-21T11:15:00', faces_count: 468 },
    { timestamp: '2023-12-21T11:00:00', faces_count: 472 },
    { timestamp: '2023-12-21T10:45:00', faces_count: 491 },
    { timestamp: '2023-12-21T10:30:00', faces_count: 512 },
    { timestamp: '2023-12-21T10:15:00', faces_count: 481 },
    { timestamp: '2023-12-21T10:00:00', faces_count: 469 },
    { timestamp: '2023-12-21T09:45:00', faces_count: 503 },
    { timestamp: '2023-12-21T09:30:00', faces_count: 488 },
    { timestamp: '2023-12-21T09:15:00', faces_count: 471 },
    { timestamp: '2023-12-21T09:00:00', faces_count: 288 },
    { timestamp: '2023-12-21T08:45:00', faces_count: 215 },
    { timestamp: '2023-12-21T08:30:00', faces_count: 104 },
    { timestamp: '2023-12-21T08:15:00', faces_count: 52 },
    { timestamp: '2023-12-21T08:00:00', faces_count: 10 },
    { timestamp: '2023-12-21T07:45:00', faces_count: 0 },
    { timestamp: '2023-12-21T07:30:00', faces_count: 0 },
    { timestamp: '2023-12-21T07:15:00', faces_count: 0 },
    { timestamp: '2023-12-21T07:00:00', faces_count: 0 },
  ];


  let displayLimit = 6; // Variable für die Anzeigelimit (Zu Beginn)

  // Funktion zur Formatierung des Datums aus dem Zeitstempel.
  // Verwendet das deutsche Datumsformat.
  const formatDate = (timestamp) => {
    const date = new Date(timestamp);
    return date.toLocaleDateString('de-DE');
  };

  // Funktion zur Formatierung der Uhrzeit aus dem Zeitstempel.
  // Verwendet das deutsche Zeitformat und zeigt Stunden, Minuten und Sekunden an.
  const formatTime = (timestamp) => {
    const time = new Date(timestamp);
    return time.toLocaleTimeString('de-DE', {
      hour: '2-digit',
      minute: '2-digit',
      second: '2-digit'
    });
  };

  // Funktion zum Laden weiterer Daten
  // Erhöht 'displayLimit' um 6 bei jedem Aufruf.
  const loadMore = () => {
    displayLimit += 6;
    if (displayLimit >= 30) {
      displayLimit = data.length
    }
  };
</script>

<style>
  .chart-container {
    width: 30%; /* Setzt die Breite des Containers auf 30% */
    margin: auto; /* Zentriert den Container horizontal */
  }
</style>

<!-- HTML-Struktur für die Darstellung der Daten in einer Tabelle -->
<h3 style="text-align:center">Historie Personenanzahl: Tabelle</h3>
<div class="chart-container">
  <!-- Bedingte Anzeige: Wenn Daten vorhanden sind, wird die Tabelle angezeigt -->
  {#if data.length > 0}
    <table class="table table-striped table-bordered">
      <thead class="thead-dark">
        <tr>
          <th>Datum</th>
          <th>Uhrzeit</th>
          <th>Gemeldete Personenanzahl</th>
        </tr>
      </thead>
      <tbody>
        <!-- Schleife über die Daten, beschränkt auf 'displayLimit' -->
        {#each data.slice(0, displayLimit) as item}
          <tr>
            <!-- Anzeige des formatierten Datums, der Zeit und der Personenanzahl für jeden Datensatz -->
            <td>{formatDate(item.timestamp)}</td>
            <td>{formatTime(item.timestamp)}</td>
            <td>{item.faces_count}</td>
          </tr>
        {/each}
      </tbody>
    </table>
    <!-- Anzeige eines "Mehr laden"-Buttons, falls nicht alle Daten angezeigt werden -->
    {#if data.length > displayLimit}
      <button class="btn btn-primary" on:click={loadMore}>Mehr laden</button>
    {/if}
  {:else}
    <div class="alert alert-info">Keine Daten vorhanden</div>
  {/if}
  <a href="/">Link zu Rohdaten (JSON)</a>
</div>
