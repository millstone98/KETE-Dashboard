<script>
  // Importieren der benötigten Module aus Svelte und Axios
  import axios from 'axios';
  import { onMount } from 'svelte';

  // Initialisierung von Variablen
  let data = []; // Array für die Daten
  let error = null; // Variable für Fehlermeldungen
  let displayLimit = 6; // Anfangslimit für die Anzeige von Datensätzen

  // URL der API für die Datenabfrage der Kamera
  const API_URL = 'https://657ca02c853beeefdb99bbf0.mockapi.io/face_count';

  // Funktion, die beim Laden der Komponente ausgeführt wird
  onMount(() => {
    // Asynchroner API-Aufruf mit Axios
    axios.get(API_URL)
      .then(response => {
        // Überprüfen, ob Daten vorhanden sind und sortieren der Daten nach Zeitstempel
        if (response.data && response.data.length > 0) {
          data = response.data.sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp));
        }
      })
      .catch(err => {
        // Fehlerbehandlung
        error = err;
      });
  });

  // Funktionen zur Formatierung von Datum und Uhrzeit
  const formatDate = (timestamp) => {
    const date = new Date(timestamp);
    return date.toLocaleDateString('de-DE');
  };

  const formatTime = (timestamp) => {
    const time = new Date(timestamp);
    return time.toLocaleTimeString('de-DE', {
      hour: '2-digit',
      minute: '2-digit',
      second: '2-digit'
    });
  };

  // Funktion zum Laden weiterer Daten
  const loadMore = () => {
    displayLimit += 6; // Erhöhen des Anzeigelimits
    if (displayLimit >= 30) {
      displayLimit = data.length; // Limit an die Gesamtanzahl der Daten anpassen
    }
  };
</script>

<style>
  .chart-container {
    width: 30%;       /* Setzt die Breite des Containers auf 30% */
    margin: auto;     /* Zentriert den Container horizontal */
  }
</style>

<h3 style="text-align:center">Historie Personenanzahl: Tabelle</h3>
<div class="chart-container">
  <!-- Bedingte Anweisungen zur Steuerung der Anzeige -->
  {#if data.length > 0}
    <!-- Tabelle zur Darstellung der Daten -->
    <table class="table table-striped table-bordered">
      <thead class="thead-dark">
        <tr>
          <th>Datum</th>
          <th>Uhrzeit</th>
          <th>Gemeldete Personenanzahl</th>
        </tr>
      </thead>
      <tbody>
        <!-- Schleife über die Daten zur Erzeugung der Tabellenzeilen -->
        {#each data.slice(0, displayLimit) as item}
          <tr>
            <td>{formatDate(item.timestamp)}</td>
            <td>{formatTime(item.timestamp)}</td>
            <td>{item.faces_count}</td>
          </tr>
        {/each}
      </tbody>
    </table>
    <!-- Button zum Laden weiterer Daten, falls verfügbar -->
    {#if data.length > displayLimit}
      <button class="btn btn-primary" on:click={loadMore}>Mehr laden</button>
    {/if}
  {:else if error}
    <!-- Anzeige einer Fehlermeldung, falls ein Fehler auftritt -->
    <div class="alert alert-danger">Fehler beim Laden der Daten: {error.message}</div>
  {:else}
    <!-- Anzeige einer Ladeanzeige, solange Daten geladen werden -->
    <div class="alert alert-info">Lade Daten...</div>
  {/if}
  <a href="https://657ca02c853beeefdb99bbf0.mockapi.io/face_count">Link zu Rohdaten (JSON)</a>
</div>