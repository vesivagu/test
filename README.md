<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Underscore.js Complex Template Example</title>
  <!-- Include jQuery -->
  <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
  <!-- Include Underscore.js -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/underscore.js/1.13.1/underscore-min.js"></script>
</head>
<body>

<div id="output"></div>

<!-- Underscore Template -->
<script type="text/template" id="template">
  <h2><%= title %></h2>
  
  <!-- Check if there are items -->
  <% if (items.length > 0) { %>
    <ul>
      <% _.each(items, function(item) { %>
        <li><%= item.name %> - <%= item.price %></li>
      <% }); %>
    </ul>
  <% } else { %>
    <p>No items available</p>
  <% } %>
</script>

<script>
  $(document).ready(function() {
    // Sample data for rendering the template
    const data = {
      title: 'Product List',
      items: [
        { name: 'Product 1', price: '$10' },
        { name: 'Product 2', price: '$15' },
        { name: 'Product 3', price: '$20' }
      ]
    };

    // Get the HTML of the template
    const templateSource = $('#template').html();

    // Compile the template using Underscore.js
    const compiledTemplate = _.template(templateSource);

    // Render the template with the provided data
    const renderedHtml = compiledTemplate(data);

    // Inject the rendered HTML into the DOM
    $('#output').html(renderedHtml);
  });
</script>

</body>
</html>
