<script>
  // Import von Axios zur Durchführung von HTTP-Anfragen und 'onMount' von Svelte für Lifecycle-Hooks (Aktionen ausführen, die nur einmal ausgeführt werden sollen, nachdem die Komponente zum ersten Mal angezeigt wird.).
  import axios from 'axios';
  import { onMount } from 'svelte';
  import '../styles/tile.css'; 

  // Deklaration von Variablen zur Speicherung der Wetterdaten und Fehlermeldungen.
  let outdoorWeatherData = null;
  let error = null;

  // Konstanten für den API-Aufruf.
  const API_KEY = '62238968e446399c7c0f71e4e810d750'; // API-Schlüssel
  const LAT = '47.172'; // Breitengrad
  const LON = '9.473'; // Längengrad
  const UNITS = 'metric'; // Grad Celsius
  const LANG = 'de' // Sprache der Wetterbeschreibung
  const URL = `https://api.openweathermap.org/data/2.5/weather?lat=${LAT}&lon=${LON}&appid=${API_KEY}&units=${UNITS}&lang=${LANG}`;

  onMount(() => {
    // Durchführen eines GET-Requests an die OpenWeatherMap-API.
    axios.get(URL)
      .then(response => {
        outdoorWeatherData = response.data;
      })
      .catch(err => {
        error = err;
      });
  });

  // Funktionen zur Formatierung von Zeit- und Datumsangaben (Umwandlung unixTimestamp in "lesbare" Zeit).
  function formatTime(unixTimestamp) {
    const date = new Date(unixTimestamp * 1000);
    return date.toLocaleTimeString(); 
  }

  function formatDate(unixTimestamp) {
    const date = new Date(unixTimestamp * 1000);
    return date.toLocaleDateString(); 
  }
</script>

<!-- Darstellung der Wetterdaten im GUI. -->
{#if outdoorWeatherData}
  <h3 style="text-align:center">Wetter jetzt</h3>
  <div class="tile">
      <!-- Anzeige verschiedener Wetterinformationen wie Ort, Temperatur, Beschreibung etc. -->
      <p>Ort: {outdoorWeatherData.name}</p>
      <p>Aktuelle Aussentemperatur: {outdoorWeatherData.main.temp}°C</p>
      <p>Wetter: {outdoorWeatherData.weather[0].description}</p>
      <!-- Anzeige des Wetter-Icons -->
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
  <div class="loading">Lade Wetterdaten...</div>
{/if}
