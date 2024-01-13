<script>

  //in Praxis durch API ersetzen.
  const modules = [
    { date: "21.12.2023", time: "09:15 - 12:30", moduleName: "KETE", teacher: "Benninger", expectedCount: 30 },
    { date: "21.12.2023", time: "13:15 - 16:30", moduleName: "ITMA", teacher: "Grivas", expectedCount: 20 },
    // weitere Module 
  ];

</script>
<h3>Stundenplan (Soll-Belegung)</h3>
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
          <td>{module.date}</td>
          <td>{module.time}</td>
          <td>{module.moduleName}</td>
          <td>{module.teacher}</td>
          <td>{module.expectedCount}</td>
        </tr>
      {/each}
    </tbody>
  </table>
  <button class="btn btn-primary">Mehr laden</button>
</div>
