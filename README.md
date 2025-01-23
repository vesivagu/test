function buildTmplFn(templateString) {
    // Parse the template string and replace expressions like ${variable}
    return function (data) {
        return templateString.replace(/\$\{([\w\.]+)\}/g, function (match, key) {
            // Traverse object properties (e.g., `data.user.name`)
            var keys = key.split('.');
            var value = data;
            for (var i = 0; i < keys.length; i++) {
                if (value[keys[i]] !== undefined) {
                    value = value[keys[i]];
                } else {
                    return ''; // If a key is missing, return an empty string
                }
            }
            return value;
        });
    };
}

// Example usage
var templateString = '<h1>${title}</h1><p>${description}</p>';
var compiled = buildTmplFn(templateString);

var data = {
    title: "Hello, World!",
    description: "This is a safer template example."
};

console.log(compiled(data));
// Output: <h1>Hello, World!</h1><p>This is a safer template example.</p>
