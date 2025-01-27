<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mustache.js Example</title>
  <!-- Include Mustache.js from CDN -->
  <script src="https://cdn.jsdelivr.net/npm/mustache@4.2.0/mustache.min.js"></script>
</head>
<body>

  <!-- Define an HTML Template with Mustache Syntax -->
  <div id="template">
    <h1>{{title}}</h1>
    <p>{{description}}</p>
  </div>

  <!-- Render the template dynamically with data -->
  <div id="output"></div>

  <script>
    // Define the data to replace in the template
    const data = {
      title: "Mustache.js Template Example",
      description: "This example shows how to use Mustache.js with CDN to render templates dynamically."
    };

    // Get the template from the DOM
    const template = document.getElementById("template").innerHTML;

    // Render the template with Mustache.js and the data
    const rendered = Mustache.render(template, data);

    // Output the rendered HTML to the DOM
    document.getElementById("output").innerHTML = rendered;
  </script>

</body>
</html>
