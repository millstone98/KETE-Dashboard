<script>
  import axios from 'axios';
  import { onMount } from 'svelte';
  import '../styles/tile.css'; 

  let latestData = null;
  let error = null;

  const API_URL = 'https://657ca02c853beeefdb99bbf0.mockapi.io/face_count';

  onMount(() => {
    axios.get(API_URL)
      .then(response => {
        if (response.data && response.data.length > 0) {
          // Sortieren der Daten, um den neuesten Eintrag zu finden
          const sortedData = response.data.sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp));
          latestData = sortedData[0];
        }
      })
      .catch(err => {
        error = err;
      });
  });

  const formatTimestamp = (timestamp) => {
    const date = new Date(timestamp);
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
  <div class="tile">
    <p>Zuletzt gemeldete Personenanzahl: {latestData.faces_count}</p>
    <p>Zeit: {formatTimestamp(latestData.timestamp)}</p>
  </div>
{:else if error}
  <div class="error">Fehler beim Laden der Daten: {error.message}</div>
{:else}
  <div class="loading">Lade Personendaten...</div>
{/if}
