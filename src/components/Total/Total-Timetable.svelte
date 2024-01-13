<script>
  const modules = [
    { date: "21.12.2023", time: "09:15 - 12:30", expectedCount: 602 },
    { date: "21.12.2023", time: "13:15 - 16:30", expectedCount: 541 },
    // weitere Module. In Praxis durch API ersetzen
  ];

  const currentDate = new Date().toLocaleDateString('de-DE');
</script>
<h3>Total: Soll-Belegung gemäss allen Stundenplänen</h3>
<div class="timetable-container">
  <table class="table table-striped table-bordered">
    <thead class="thead-dark">
      <tr>
        <th>Datum</th>
        <th>Uhrzeit</th>
        <th>Erwartete Personen</th>
      </tr>
    </thead>
    <tbody>
      {#each modules as module}
        <tr>
          <td>{module.date}</td>
          <td>{module.time}</td>
          <td>{module.expectedCount}</td>
        </tr>
      {/each}
    </tbody>
  </table>
  <button class="btn btn-primary">Mehr laden</button>
</div>
