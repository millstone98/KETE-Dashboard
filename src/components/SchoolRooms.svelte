<script>
  const schoolrooms = [
    { name: "SW101", size: "150m", actual: 5, planned: 20},
    { name: "SW102", size: "70m", actual: 20, planned: 30},
    {name: "SW103", size: "109m", actual: 6, planned: 9}, {name: "SW104", size: "120m", actual: 2, planned: 9}, {name: "SW105", size: "133m", actual: 6, planned: 6}, {name: "SW106", size: "98m", actual: 6, planned: 5}, {name: "SW107", size: "95m", actual: 6, planned: 9}, {name: "SW108", size: "142m", actual: 6, planned: 9}, {name: "SW109", size: "115m", actual: 6, planned: 9}, {name: "SW110", size: "147m", actual: 6, planned: 9}, {name: "SW111", size: "109m", actual: 6, planned: 9}, {name: "SW112", size: "71m", actual: 6, planned: 9}, {name: "SW113", size: "118m", actual: 6, planned: 7}, {name: "SW114", size: "103m", actual: 6, planned: 7}, {name: "SW115", size: "113m", actual: 6, planned: 9}, {name: "SW116", size: "122m", actual: 6, planned: 9}, {name: "SW117", size: "134m", actual: 6, planned: 9}, {name: "SW118", size: "114m", actual: 2, planned: 7}, {name: "SW119", size: "78m", actual: 3, planned: 6}, {name: "SW120", size: "81m", actual: 1, planned: 8}, {name: "SW121", size: "94m", actual: 6, planned: 9}, {name: "SW201", size: "148m", actual: 6, planned: 4}, {name: "SW202", size: "83m", actual: 6, planned: 5}, {name: "SW203", size: "117m", actual: 6, planned: 3}, {name: "SW204", size: "74m", actual: 6, planned: 9}, {name: "SW205", size: "98m", actual: 6, planned: 9}, {name: "SW206", size: "92m", actual: 6, planned: 9}, {name: "SW207", size: "107m", actual: 6, planned: 9}, {name: "SW208", size: "102m", actual: 6, planned: 9}, {name: "SW209", size: "101m", actual: 6, planned: 9}, {name: "SW210", size: "85m", actual: 6, planned: 9}, {name: "SW211", size: "146m", actual: 6, planned: 9}, {name: "SW212", size: "87m", actual: 6, planned: 9}, {name: "SW213", size: "73m", actual: 6, planned: 9}, {name: "SW214", size: "98m", actual: 6, planned: 9}, {name: "SW215", size: "79m", actual: 6, planned: 9}, {name: "SW216", size: "92m", actual: 6, planned: 9}, {name: "SW217", size: "92m", actual: 6, planned: 8}, {name: "SW218", size: "145m", actual: 6, planned: 8}, {name: "SW219", size: "143m", actual: 6, planned: 8}, {name: "SW220", size: "84m", actual: 6, planned: 8}, {name: "SW221", size: "115m", actual: 6, planned: 8}, {name: "SW301", size: "138m", actual: 6, planned: 8}, {name: "SW302", size: "127m", actual: 7, planned: 8}, {name: "SW303", size: "81m", actual: 6, planned: 8}, {name: "SW304", size: "125m", actual: 6, planned: 8}, {name: "SW305", size: "116m", actual: 6, planned: 8}, {name: "SW306", size: "146m", actual: 6, planned: 8}, {name: "SW307", size: "89m", actual: 7, planned: 8}, {name: "SW308", size: "78m", actual: 6, planned: 8}, {name: "SW309", size: "73m", actual: 6, planned: 8}, {name: "SW310", size: "117m", actual: 6, planned: 8}, {name: "SW311", size: "80m", actual: 7, planned: 8}, {name: "SW312", size: "74m", actual: 6, planned: 8}, {name: "SW313", size: "134m", actual: 6, planned: 8}, {name: "SW314", size: "97m", actual: 6, planned: 8}, {name: "SW315", size: "94m", actual: 6, planned: 8}, {name: "SW316", size: "84m", actual: 6, planned: 8}, {name: "SW317", size: "102m", actual: 6, planned: 8}, {name: "SW318", size: "85m", actual: 6, planned: 8}, {name: "SW319", size: "80m", actual: 6, planned: 8}, {name: "SW320", size: "118m", actual: 6, planned: 8}, {name: "SW321", size: "146m", actual: 6, planned: 8}
    // weitere Räume 
  ];

   // Berechne die Summen für 'actual' und 'planned'
  const totalActual = schoolrooms.reduce((sum, schoolroom) => sum + schoolroom.actual, 0);
  const totalPlanned = schoolrooms.reduce((sum, schoolroom) => sum + schoolroom.planned, 0);
</script>



<div class="timetable-container">
  <table class="table table-striped table-bordered">
    <thead class="thead-dark">
      <tr>
        <th>Raumbezeichnung</th>
        <th>Raumgrösse</th>
        <th>Ist-Belegung</th>
        <th>Soll-Belegung</th>
      </tr>
    </thead>
    <tbody>
      {#each schoolrooms as schoolroom}
        <tr>
          <td><a href="/{schoolroom.name}">{schoolroom.name}</a></td>
          <td>{schoolroom.size}<sup>2</sup></td>
          <td>{schoolroom.actual}</td>
          <td>{schoolroom.planned}</td>
        </tr>
      {/each}
          <!-- Zeile für die Summe -->
    <tr>
      <td><b>Gesamt</b></td>
      <td><b>-</b></td>
      <td><b>{totalActual}</b></td>
      <td><b>{totalPlanned}</b></td>
    </tr>
    </tbody>
  </table>
</div>
