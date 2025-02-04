<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mustache.js Complex Logic with Select Example</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/mustache.js/4.2.0/mustache.min.js"></script>
</head>
<body>
  <!-- Template -->
  <script id="template" type="x-tmpl-mustache">
    <h1>{{title}}</h1>
    <p>{{message}}</p>

    <!-- Dropdown (select list) populated from options -->
    <label for="userSelect">Choose a user:</label>
    <select id="userSelect">
      {{#users}}
        <option value="{{id}}">{{name}} ({{age}} years old)</option>
      {{/users}}
    </select>

    <!-- Conditional message based on selection -->
    <div id="message"></div>
  </script>

  <!-- Container to render the content -->
  <div id="content"></div>

  <script>
    $(document).ready(function () {
      // Example data to pass to the template
      var data = {
        title: "Mustache.js Select List Example",
        message: "Please choose a user from the dropdown.",
        users: [
          { id: 1, name: "John Doe", age: 28 },
          { id: 2, name: "Jane Smith", age: 34 },
          { id: 3, name: "Sara Lee", age: 22 }
        ]
      };

      // Render the Mustache template with the data
      var template = $('#template').html();
      var rendered = Mustache.render(template, data);
      $('#content').html(rendered);

      // Event handler for select list change
      $('#userSelect').on('change', function() {
        var selectedUserId = $(this).val();
        var selectedUser = data.users.find(user => user.id == selectedUserId);

        // Display a message based on the selected user
        if (selectedUser) {
          $('#message').html('<p>You selected ' + selectedUser.name + ', who is ' + selectedUser.age + ' years old.</p>');
        }
      });
    });
  </script>
</body>
</html>
