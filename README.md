<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Nunjucks.js with jQuery Example</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/nunjucks/3.2.3/nunjucks.min.js"></script>
</head>
<body>
  <!-- Template -->
  <script id="template" type="text/nunjucks">
    <h1>{{ title }}</h1>
    <p>{{ message }}</p>
    
    <ul>
      {% for user in users %}
        <li>{{ user.name }} - {{ user.age }} years old</li>
      {% else %}
        <li>No users available</li>
      {% endfor %}
    </ul>

    {% if showSpecialMessage %}
      <div class="special-message">This is a special message!</div>
    {% endif %}
  </script>

  <!-- Container to render the content -->
  <div id="content"></div>

  <script>
    $(document).ready(function () {
      // Example data to pass to the template
      var data = {
        title: "Nunjucks.js Example",
        message: "This is a complex Nunjucks template with logic.",
        users: [
          { name: "John Doe", age: 28 },
          { name: "Jane Smith", age: 34 },
          { name: "Sara Lee", age: 22 }
        ],
        showSpecialMessage: true // You can toggle this to false to hide the special message
      };

      // Configure Nunjucks to use the DOM for templates
      nunjucks.configure({ autoescape: true });

      // Get the template
      var template = $('#template').html();

      // Render the template with the data
      var rendered = nunjucks.renderString(template, data);

      // Inject the rendered content into the #content div
      $('#content').html(rendered);
    });
  </script>
</body>
</html>
