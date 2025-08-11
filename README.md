# infovis

### Para obtener los datos se utilizo un comando por consola web en el sitio:
https://steamdb.info/calculator/76561199005740267/?cc=ar&all_games#games

### El comando fue:
(() => {
  const table = document.querySelector('#games table');

  const headers = Array.from(table.querySelectorAll('thead th')).map(h =>
    `"${h.innerText.replace(/"/g, '""')}"`
  ).join(',');

  const rows = Array.from(table.querySelectorAll('tbody tr')).map(r =>
    Array.from(r.querySelectorAll('td')).map(cell =>
      `"${cell.innerText.replace(/"/g, '""')}"`
    ).join(',')
  );

  const csvContent = [headers, ...rows].join('\n');

  // Add UTF-8 BOM so Excel interprets accents correctly
  const blob = new Blob(["\uFEFF" + csvContent], { type: 'text/csv;charset=utf-8;' });

  const link = document.createElement('a');
  link.href = URL.createObjectURL(blob);
  link.download = 'steam_games.csv';
  document.body.appendChild(link);
  link.click();
  document.body.removeChild(link);
})();

Y luego se realizo una leve edicion en excel para poder tener unicidad de tipo de datos.
