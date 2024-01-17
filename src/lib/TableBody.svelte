<script>
  export let type;
  export let data;
  const values = data.values;
  const rows = values;
  let tRows = [];
  let rowsTD = '';
  let colCount = rows[0].length;

  function generateRows() {
    for (var i = 1; i < rows.length; i++) {
      if (rows[i][0]) rowsTD = rowsTD + generateCols(i);
    }
    return rowsTD;
  }  

  function generateCols(i) {
    const firstName = rows[i][1] ? rows[i][1] : '***********';
    const lastName = rows[i][2] ? rows[i][2] : '';
    const name = firstName + ' ' + lastName;
    const phone = rows[i][5] ? rows[i][5] : '';
    const email = rows[i][3] ? rows[i][3] : '';
    const address = rows[i][4] ? rows[i][4] : '';
    let trs;
    switch (type) {
      case 'playerinfo':
        trs = `<tr><th scope='row'>${name}</th><td>${phone}</td>`
        trs = trs + '</tr><tr>'
        trs = trs + `<td>${email}</td><td>${address}</td>`
        trs = trs + '</tr>'
        return trs;        
        break;    
      default: 

          trs =`<tr><th scope='row'>${name}</th>`;

          for (var j = 1; j < colCount - 1; j++) {
            let val = rows[i][j + 2] ? rows[i][j + 2] : '';
            trs = trs + `<td data-val=${val}></td>`;
          }
          trs = trs + '</tr>'
          return trs;
        break;
    }

  }
  </script>
  
  <tbody>
    {@html `${generateRows()}`}
  </tbody>