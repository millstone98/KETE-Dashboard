<script>
  const modules = [
    { time: "09:15 - 12:30", moduleName: "KETE", teacher: "Benninger", expectedCount: 30 },
    { time: "13:15 - 16:30", moduleName: "ITMA", teacher: "Grivas", expectedCount: 25 },
    // weitere Module 
  ];

  const currentDate = new Date().toLocaleDateString('de-DE');
</script>

<style>
  .timetable-container {
    width: 50%;
    margin: auto;
  }
</style>

<div class="timetable-container">
  <table class="table table-striped table-bordered">
    <thead class="thead-dark">
      <tr>
        <th>Datum</th>
        <th>Uhrzeit</th>
        <th>Modulname</th>
        <th>Dozent</th>
        <th>Erwartete Personen</th>
      </tr>
    </thead>
    <tbody>
      {#each modules as module}
        <tr>
          <td>{currentDate}</td>
          <td>{module.time}</td>
          <td>{module.moduleName}</td>
          <td>{module.teacher}</td>
          <td>{module.expectedCount}</td>
        </tr>
      {/each}
    </tbody>
  </table>
</div>
