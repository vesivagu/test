const express = require('express');
const path = require('path');
const fs = require('fs');

const app = express();
const PORT = process.env.PORT || 8080;

// Enable JSON body parsing
app.use(express.json());

// Load mock API definitions
const mockData = require('./mock-data.json');

// Register mock routes
for (const [route, methods] of Object.entries(mockData)) {
  for (const [method, { request, response }] of Object.entries(methods)) {
    app[method.toLowerCase()](route, (req, res) => {
      if (request && JSON.stringify(req.body) !== JSON.stringify(request)) {
        return res.status(400).json({ error: 'Invalid request body' });
      }
      res.json(response);
    });
  }
}

// Serve Angular static files
const angularDistPath = path.join(__dirname, 'dist/your-angular-app-name');
app.use(express.static(angularDistPath));

// Redirect all other routes to Angular index.html
app.get('*', (req, res) => {
  res.sendFile(path.join(angularDistPath, 'index.html'));
});

// Start server
app.listen(PORT, '0.0.0.0', () => {
  console.log(`App + Mock API running on http://0.0.0.0:${PORT}`);
});
