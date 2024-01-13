<script>
  import Header from './components/Header.svelte';
  import Footer from './components/Footer.svelte';
  import Weather from './components/Weather.svelte';
  import WeatherForecast from './components/WeatherForecast.svelte'

  import TotalStudentCountTile from './components/Total/Total-StudentCountTile.svelte';
  import TotalHistoryTable from './components/Total/Total-History-Table.svelte';
  import TotalHistoryChart from './components/Total/Total-History-Chart.svelte';
  import TotalTimeTable from './components/Total/Total-Timetable.svelte';
  import SchoolRooms from './components/Total/SchoolRooms.svelte';
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
            <TotalStudentCountTile />
          </div>
          <div class="col">
            <TotalTimeTable />
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
        <TotalHistoryChart />
        <TotalHistoryTable />
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
            <Weather />
          </div>
          <div class="col">
            <WeatherForecast />
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<Footer />