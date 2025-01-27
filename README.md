<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mustache.js Example</title>
    <!-- Include Mustache.js CDN -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mustache.js/4.2.0/mustache.min.js"></script>
</head>
<body>

    <!-- The template with Mustache syntax -->
    <script id="template" type="x-tmpl-mustache">
        <div>
            <h1>{{title}}</h1>
            <p>{{description}}</p>
        </div>
    </script>

    <div id="content"></div>

    <script>
        // The data to be injected into the template
        const data = {
            title: "Welcome to Mustache.js",
            description: "This is an example of using Mustache.js with a CDN."
        };

        // Get the template from the DOM
        const template = document.getElementById('template').innerHTML;

        // Render the template with data
        const rendered = Mustache.render(template, data);

        // Inject the rendered HTML into the page
        document.getElementById('content').innerHTML = rendered;
    </script>

</body>
</html>
