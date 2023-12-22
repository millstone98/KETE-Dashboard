<script>
    import Header from './components/Header.svelte';
    import Footer from './components/Footer.svelte';
    import ITemperatureTile from './components/ITemperatureTile.svelte';
    import OTemperatureTile from './components/OTemperatureTile.svelte';
    import StudentCountTile from './components/StudentCountTile.svelte';
    import StudentCountTileTable from './components/StudentCountTileTable.svelte';
    import ChartTile from './components/ChartTile.svelte';
    import Timetable from './components/Timetable.svelte';
    import ostlogo from './assets/ost.svg';
  </script>
  
  <style>
    .dashboard {
      grid-template-columns: repeat(auto-fill);
      padding: 20px;
      justify-content: center; /* Zentriert die Tiles horizontal */
    }
    h1 {
        font-family: 'Roboto', sans-serif;
        text-align: center;
    }
  </style>
  
  <Header />

  <h1>Temperaturjustage SW202</h1>
  <img src={ostlogo} alt="OST Logo" style="display: block; margin: 0 auto; vertical-align: middle;">
  
  <div class="dashboard">
    <OTemperatureTile />
    <Timetable />
    <StudentCountTile />
    <StudentCountTileTable />
    <ChartTile />
    <ITemperatureTile />
    <!-- Weitere Kacheln hier hinzufügen -->
  </div>
  
  <Footer />
  
  