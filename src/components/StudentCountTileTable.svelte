<script>
  import axios from 'axios';
  import { onMount } from 'svelte';

  let data = [];
  let error = null;
  let displayLimit = 6; // Variable für die Anzeigelimit

  const API_URL = 'https://657ca02c853beeefdb99bbf0.mockapi.io/face_count';

  onMount(() => {
    axios.get(API_URL)
      .then(response => {
        if (response.data && response.data.length > 0) {
          data = response.data.sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp));
        }
      })
      .catch(err => {
        error = err;
      });
  });

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
    displayLimit += 6;
    if (displayLimit >= 30) {
      displayLimit = data.length
    }
  };
</script>
<style>
  .chart-container {
    width: 30%;       /* Setzt die Breite des Containers auf 80% */
    margin: auto;     /* Zentriert den Container horizontal */
  }
</style>
<h3 style="text-align:center">Historie Personenanzahl: Tabelle</h3>
<div class="chart-container">
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
        {#each data.slice(0, displayLimit) as item}
          <tr>
            <td>{formatDate(item.timestamp)}</td>
            <td>{formatTime(item.timestamp)}</td>
            <td>{item.faces_count}</td>
          </tr>
        {/each}
      </tbody>
    </table>
    {#if data.length > displayLimit}
    <button class="btn btn-primary" on:click={loadMore}>Mehr laden</button>
    {/if}
  {:else if error}
    <div class="alert alert-danger">Fehler beim Laden der Daten: {error.message}</div>
  {:else}
    <div class="alert alert-info">Lade Daten...</div>
  {/if}
  <a href="https://657ca02c853beeefdb99bbf0.mockapi.io/face_count">Link zu Rohdaten (JSON)</a>
</div>