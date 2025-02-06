const fs = require('fs');
const path = require('path');

// Path to the Angular package.json file
const packageJsonPath = path.join(__dirname, 'package.json');

// Read the package.json file
fs.readFile(packageJsonPath, 'utf8', (err, data) => {
    if (err) {
        console.error('Error reading package.json:', err);
        return;
    }

    try {
        // Parse JSON data
        let packageJson = JSON.parse(data);

        // Update the project name
        packageJson.name = 'new-project-name'; // Change to the desired name

        // Convert JSON back to a string
        const updatedData = JSON.stringify(packageJson, null, 2);

        // Write the updated JSON back to package.json
        fs.writeFile(packageJsonPath, updatedData, 'utf8', (err) => {
            if (err) {
                console.error('Error writing package.json:', err);
            } else {
                console.log('Project name updated successfully!');
            }
        });
    } catch (error) {
        console.error('Error parsing package.json:', error);
    }
});
