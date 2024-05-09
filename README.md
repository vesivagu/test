To generate JSON based on a custom JSON schema using npm, you can use libraries like `json-schema-faker` or `faker.js` along with `json-schema` for schema validation. First, install the required packages:

```bash
npm install json-schema-faker faker json-schema
```

Then, you can use them in your code like this:

```javascript
const jsf = require('json-schema-faker');
const faker = require('faker');
const schema = require('./your-custom-schema.json'); // Import your custom JSON schema

jsf.extend('faker', () => faker);

jsf.resolve(schema).then(sample => {
  console.log(JSON.stringify(sample, null, 2));
});
```

Replace `'./your-custom-schema.json'` with the path to your custom JSON schema file. This code will generate a JSON object based on your schema using fake data provided by `faker.js`.
