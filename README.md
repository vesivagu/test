var source = $("#template").html();
var template = Handlebars.compile(source);
var data = { title: "Hello", description: "World" };
var html = template(data);
$("#output").html(html);



<script id="template" type="text/x-handlebars-template">
    <h1>{{title}}</h1>
    <p>{{description}}</p>
</script>
<div id="output"></div>
