<!DOCTYPE html>
<html>
<head>
  <title>Complex Hierarchy Object to Table</title>
  <style>
    table {
      border-collapse: collapse;
      width: 100%;
    }
    th, td {
      border: 1px solid black;
      padding: 8px;
      text-align: left;
    }
  </style>
</head>
<body>
  <div id="table-container"></div>

  <script>
    function createTable(data, parentKey = "") {
      let html = `<table>`;

      for (const key in data) {
        if (data.hasOwnProperty(key)) {
          const value = data[key];
          const currentKey = parentKey ? `${parentKey}.${key}` : key;

          if (typeof value === "object" && !Array.isArray(value)) {
            html += `<tr><th>${currentKey}</th><td>${createTable(value, currentKey)}</td></tr>`;
          } else {
            html += `<tr><th>${currentKey}</th><td>${value}</td></tr>`;
          }
        }
      }

      html += `</table>`;
      return html;
    }

    const data = {
      // Your hierarchical object here...
    };

    const tableContainer = document.getElementById("table-container");
    tableContainer.innerHTML = createTable(data);
  </script>
</body>
</html>
