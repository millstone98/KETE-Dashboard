<script>
  // Importieren von Axios für HTTP-Anfragen und onMount von Svelte für Lifecycle-Hooks.
  import axios from 'axios';
  import { onMount } from 'svelte';
  import '../../styles/tile.css'; 

  // Initialisierung von Variablen für die neuesten Daten und Fehler.
  let latestData = null;
  let error = null;

  // API-URL zur Abfrage von Daten der Kamera.
  const API_URL = 'https://657ca02c853beeefdb99bbf0.mockapi.io/face_count';

  // Funktion, die beim Laden der Komponente ausgeführt wird.
  onMount(() => {
    // API-Anfrage mit Axios, um Daten zu erhalten.
    axios.get(API_URL)
      .then(response => {
        // Überprüfen, ob Daten vorhanden sind und Sortieren der Daten nach Zeitstempel.
        if (response.data && response.data.length > 0) {
          const sortedData = response.data.sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp));
          // Speichern des neuesten Datensatzes.
          latestData = sortedData[0];
        }
      })
      .catch(err => {
        // Fehlerbehandlung, falls ein Fehler bei der Anfrage auftritt.
        error = err;
      });
  });

  // Funktion zur Formatierung des Zeitstempels.
  const formatTimestamp = (timestamp) => {
    const date = new Date(timestamp);
    // Rückgabe des formatierten Zeitstempels im gewünschten Format.
    return date.toLocaleDateString('de-DE', {
      day: '2-digit',
      month: '2-digit',
      year: 'numeric',
      hour: '2-digit',
      minute: '2-digit',
      second: '2-digit'
    });
  };
</script>

{#if latestData}
  <!-- Anzeigen der neuesten Daten, wenn diese vorhanden sind. -->
  <h3 style="text-align:center">Personen jetzt (Ist-Belegung)</h3>
  <div class="tile">
    <!-- Anzeige der letzten gemeldeten Personenanzahl und des Zeitpunkts. -->
    <p>Zuletzt gemeldete Personenanzahl: {latestData.faces_count}</p>
    <p>Zeit: {formatTimestamp(latestData.timestamp)}</p>
    <!-- Link zu den Rohdaten im JSON-Format. -->
    <a href="https://657ca02c853beeefdb99bbf0.mockapi.io/face_count">Link zu Rohdaten (JSON)</a>
  </div>
{:else if error}
  <!-- Anzeige einer Fehlermeldung, falls ein Fehler aufgetreten ist. -->
  <div class="error">Fehler beim Laden der Daten: {error.message}</div>
{:else}
  <!-- Anzeige einer Ladeanzeige, während die Daten geladen werden. -->
  <div class="loading">Lade Personendaten...</div>
{/if}
