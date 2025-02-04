<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Mustache.js with jQuery Example</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/mustache@4.2.0/mustache.min.js"></script>
</head>
<body>
    <h1>User List</h1>
    
    <!-- Mustache Template -->
    <script id="user-template" type="x-tmpl-mustache">
        <ul>
            {{#users}}
                <li>{{name}} - {{email}}</li>
            {{/users}}
        </ul>
    </script>

    <!-- Container to render the template -->
    <div id="user-list"></div>

    <script>
        $(document).ready(function () {
            // Sample data
            var data = {
                users: [
                    { name: "Alice", email: "alice@example.com" },
                    { name: "Bob", email: "bob@example.com" },
                    { name: "Charlie", email: "charlie@example.com" }
                ]
            };

            // Get the template from the script tag
            var template = $('#user-template').html();

            // Render the data using Mustache
            var rendered = Mustache.render(template, data);

            // Insert the rendered HTML into the DOM
            $('#user-list').html(rendered);
        });
    </script>
</body>
</html>
