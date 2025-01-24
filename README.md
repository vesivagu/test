function buildTemplate(templateString) {
    return function(data) {
        return templateString.replace(/\$\{([\w\.]+)\}/g, function(match, key) {
            var keys = key.split('.');
            var value = data;
            for (var i = 0; i < keys.length; i++) {
                if (value[keys[i]] !== undefined) {
                    value = value[keys[i]];
                } else {
                    return ''; // Handle missing keys
                }
            }
            return value;
        });
    };
}
