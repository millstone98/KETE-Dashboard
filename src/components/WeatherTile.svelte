<script>
  import axios from 'axios';
  import { onMount } from 'svelte';
  import '../styles/tile.css'; 

  let outdoorWeatherData = null;
  let error = null;

  const API_KEY = '62238968e446399c7c0f71e4e810d750'; // API-Schlüssel
  const LAT = '47.17'; // Breitengrad
  const LON = '9.47'; // Längengrad
  const UNITS = 'metric'; // Grad Celsius
  const LANG = 'de'
  const URL = `https://api.openweathermap.org/data/2.5/weather?lat=${LAT}&lon=${LON}&appid=${API_KEY}&units=${UNITS}&lang=${LANG}`;

  onMount(() => {
    axios.get(URL)
      .then(response => {
        outdoorWeatherData = response.data;
      })
      .catch(err => {
        error = err;
      });
  });

  function formatTime(unixTimestamp) {
    const date = new Date(unixTimestamp * 1000);
    return date.toLocaleTimeString(); // oder ein anderes Format nach Wunsch
  }

  function formatDate(unixTimestamp) {
    const date = new Date(unixTimestamp * 1000);
    return date.toLocaleDateString(); // oder ein anderes Format nach Wunsch
  }
</script>

{#if outdoorWeatherData}
<div class="tile">
  <p>Ort: {outdoorWeatherData.name}</p>
  <p>Aktuelle Aussentemperatur: {outdoorWeatherData.main.temp}°C</p>
  <p>Wetter: {outdoorWeatherData.weather[0].description}</p>
  <img src={`https://openweathermap.org/img/wn/${outdoorWeatherData.weather[0].icon}@2x.png`} alt="Wetter-Icon" />
  <p>Bewölkungsgrad: {outdoorWeatherData.clouds.all}%</p>
  <p>Luftfeuchtigkeit: {outdoorWeatherData.main.humidity}%</p>
  <p>Sonnenaufgang: {formatTime(outdoorWeatherData.sys.sunrise)}</p>
  <p>Sonnenuntergang: {formatTime(outdoorWeatherData.sys.sunset)}</p>
  <p>Daten übermittelt am: {formatDate(outdoorWeatherData.dt)} {formatTime(outdoorWeatherData.dt)}</p>
  <a href="https://api.openweathermap.org/data/2.5/weather?lat={LAT}&lon={LON}&appid={API_KEY}&units={UNITS}&lang={LANG}">Link zu Rohdaten (JSON)</a>
  <!-- Weitere Wetterdaten können hier angezeigt werden -->
</div>
{:else if error}
<div class="error">Fehler beim Laden der Wetterdaten: {error.message}</div>
{:else}
<div class="loading">Lade Außen-Wetterdaten...</div>
{/if}
