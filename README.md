<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>JsRender Select Example</title>
  <script src="https://cdn.jsdelivr.net/npm/jsrender"></script>
</head>
<body>

  <h2>Dynamic Select Dropdown with JsRender</h2>
  
  <!-- Template for rendering the select dropdown -->
  <script id="select-template" type="text/x-jsrender">
    <select id="dynamic-select">
      {{for options}}
        <option value="{{:value}}">{{:label}}</option>
      {{/for}}
    </select>
  </script>

  <!-- Div where the rendered dropdown will appear -->
  <div id="dropdown-container"></div>

  <script>
    // Data for the select options
    const data = {
      options: [
        { value: '1', label: 'Option 1' },
        { value: '2', label: 'Option 2' },
        { value: '3', label: 'Option 3' },
        { value: '4', label: 'Option 4' }
      ]
    };

    // Get the template by its id
    const template = $("#select-template").render(data);

    // Render the template and insert it into the dropdown container
    $("#dropdown-container").html(template);
  </script>

</body>
</html>
