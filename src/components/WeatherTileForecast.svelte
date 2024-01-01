<script>
  import axios from 'axios';
  import { onMount } from 'svelte';

  let weatherData = null;
  let error = null;
  let displayLimit = 4; // Variable für die Anzeigelimit

  const API_KEY = '62238968e446399c7c0f71e4e810d750'; // API-Schlüssel
  const LAT = '47.172'; // Breitengrad
  const LON = '9.473'; // Längengrad
  const UNITS = 'metric'; // Grad Celsius
  const LANG = 'de';
  const URL = `https://api.openweathermap.org/data/2.5/forecast?lat=${LAT}&lon=${LON}&appid=${API_KEY}&units=${UNITS}&lang=${LANG}`;

  onMount(() => {
    axios.get(URL)
      .then(response => {
        weatherData = response.data;
      })
      .catch(err => {
        error = err;
      });
  });

  const formatDate = (timestamp) => {
    const date = new Date(timestamp * 1000);
    return date.toLocaleString('de-DE', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric', hour: '2-digit', minute: '2-digit' });
  };

  // Funktion zum Laden weiterer Daten
  const loadMore = () => {
    displayLimit += 4;
    if (displayLimit >= 20) {
      displayLimit = weatherData.list.length
    }
  };
</script>

{#if weatherData}
  <div>
    <h3>Wettervorhersage für {weatherData.city.name}</h3>
    <table class="table table-striped">
      <thead>
        <tr>
          <th>Zeit</th>
          <th>Temperatur</th>
          <th>Beschreibung</th>
          <th>Luftfeuchtigkeit</th>
          <th>Bewölkung</th>
        </tr>
      </thead>
      <tbody>
        {#each weatherData.list.slice(0, displayLimit) as interval}
          <tr>
            <td>{formatDate(interval.dt)}</td>
            <td>{interval.main.temp}°C</td>
            <td>{interval.weather[0].description}</td>
            <td>{interval.main.humidity}%</td>
            <td>{interval.clouds.all}%</td>
          </tr>
        {/each}
      </tbody>
    </table>
    {#if weatherData.list.length > displayLimit}
      <button class="btn btn-primary" on:click={loadMore}>Mehr laden</button>
    {/if}
    <a href="https://api.openweathermap.org/data/2.5/forecast?lat={LAT}&lon={LON}&appid={API_KEY}&units={UNITS}&lang={LANG}">Link zu Rohdaten (JSON)</a>
  </div>
{:else if error}
  <div class="error">Fehler beim Laden der Wetterdaten: {error.message}</div>
{:else}
  <div class="loading">Lade Wetterdaten...</div>
{/if}
