<script>
  import Header from './components/Header.svelte';
  import Footer from './components/Footer.svelte';
  import WeatherTile from './components/WeatherTile.svelte';
  import StudentCountTileTotal from './components/StudentCountTileTotal.svelte';
  import StudentCountTileTable from './components/StudentCountTileTable.svelte';
  import ChartTile from './components/ChartTile.svelte';
  import WeatherTileForecast from './components/WeatherTileForecast.svelte'
  import TimetableTotal from './components/TimetableTotal.svelte';
  import SchoolRooms from './components/SchoolRooms.svelte';
</script>

<style>
  .accordion-button{
    font-size: 25px;
    background-color: rgb(215, 40, 100); 
    font: rgb(255, 255, 255);
  }

  h1 {
        font-family: 'Roboto', sans-serif;
        text-align: center;
  }

  .top{
        padding-top: 30px;
        padding-bottom: 50px;
  }
</style>


<Header />
<div class="top">
  <h1>Tatsächliche Raumnutzung - OST Buchs SG (gesamter Campus)</h1>
</div>

<div class="accordion" id="accordionPanelsStayOpenExample">
  <div class="accordion-item">
    <h2 class="accordion-header">
      <button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#panelsStayOpen-collapseOne" aria-expanded="true" aria-controls="panelsStayOpen-collapseOne">
        Aktuelle Personenanzahl
      </button>
    </h2>
    <div id="panelsStayOpen-collapseOne" class="accordion-collapse collapse show">
      <div class="accordion-body">
        <div class="row">
          <div class="col">
            <StudentCountTileTotal />
          </div>
          <div class="col">
            <TimetableTotal />
          </div>
        </div>        
      </div>
    </div>
  </div>
  <div class="accordion-item">
    <h2 class="accordion-header">
      <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#panelsStayOpen-collapseTwo" aria-expanded="false" aria-controls="panelsStayOpen-collapseTwo">
        Historie Personenanzahl
      </button>
    </h2>
    <div id="panelsStayOpen-collapseTwo" class="accordion-collapse collapse">
      <div class="accordion-body">
        <ChartTile />
        <StudentCountTileTable />
      </div>
    </div>
  </div>
  <div class="accordion-item">
    <h2 class="accordion-header">
      <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#panelsStayOpen-collapseThree" aria-expanded="false" aria-controls="panelsStayOpen-collapseThree">
        Übersicht Schulräume
      </button>
    </h2>
    <div id="panelsStayOpen-collapseThree" class="accordion-collapse collapse">
      <div class="accordion-body">
        <SchoolRooms />
      </div>
    </div>
  </div>
  <div class="accordion-item">
    <h2 class="accordion-header">
      <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#panelsStayOpen-collapseFour" aria-expanded="false" aria-controls="panelsStayOpen-collapseFour">
        Wetter
      </button>
    </h2>
    <div id="panelsStayOpen-collapseFour" class="accordion-collapse collapse">
      <div class="accordion-body">
        <div class="row">
          <div class="col">
            <WeatherTile />
          </div>
          <div class="col">
            <WeatherTileForecast />
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<Footer />