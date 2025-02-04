<div id="template" style="display: none;">
  {{#isAdmin}}
    <p>Welcome, Admin {{name}}!</p>
  {{/isAdmin}}
  
  {{^isAdmin}}
    <p>Welcome, {{name}}! You are a regular user.</p>
  {{/isAdmin}}
</div>

<div id="output"></div>



$(document).ready(function () {
  const template = $("#template").html();

  // Example 1: Admin User
  const adminData = {
    name: "Alice",
    isAdmin: true
  };
  const adminOutput = Mustache.render(template, adminData);
  $("#output").append(adminOutput);

  // Example 2: Regular User
  const userData = {
    name: "Bob",
    isAdmin: false
  };
  const userOutput = Mustache.render(template, userData);
  $("#output").append(userOutput);
});
