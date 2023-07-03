function convertObjectToTable(obj) {
  // Create the table element
  var table = document.createElement('table');
  
  // Recursive function to generate table rows
  function createRows(data, parent) {
    for (var key in data) {
      if (data.hasOwnProperty(key)) {
        var value = data[key];
        
        // Create a new row
        var row = document.createElement('tr');
        parent.appendChild(row);
        
        // Create cell for the key
        var keyCell = document.createElement('td');
        keyCell.textContent = key;
        row.appendChild(keyCell);
        
        // Create cell for the value
        var valueCell = document.createElement('td');
        row.appendChild(valueCell);
        
        // Check if the value is an object (nested structure)
        if (typeof value === 'object' && value !== null) {
          // Create a new table inside the value cell
          var nestedTable = document.createElement('table');
          valueCell.appendChild(nestedTable);
          
          // Recursively create rows for the nested object
          createRows(value, nestedTable);
        } else {
          // Otherwise, simply set the value as text content
          valueCell.textContent = value;
        }
      }
    }
  }
  
  // Start the recursive function to create table rows
  createRows(obj, table);
  
  return table;
}

// Example usage:
var data = {
  name: 'John',
  age: 30,
  address: {
    street: '123 Main St',
    city: 'New York',
    country: 'USA'
  },
  hobbies: ['reading', 'running', 'cooking']
};

var tableElement = convertObjectToTable(data);

// Add the generated table to the DOM
document.body.appendChild(tableElement);
