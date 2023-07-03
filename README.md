// Example complex JavaScript object hierarchy
const data = {
  employees: [
    {
      id: 1,
      name: 'John Doe',
      department: 'Sales',
      salary: 50000,
      address: {
        street: '123 Main St',
        city: 'New York',
        country: 'USA'
      }
    },
    {
      id: 2,
      name: 'Jane Smith',
      department: 'Marketing',
      salary: 60000,
      address: {
        street: '456 Elm St',
        city: 'San Francisco',
        country: 'USA'
      }
    }
  ]
};

// Function to convert object hierarchy to HTML table
function convertObjectToTable(data) {
  // Create the table structure
  const table = document.createElement('table');
  
  // Create the table header row
  const thead = document.createElement('thead');
  const headerRow = document.createElement('tr');
  
  // Extract the headers from the first object in the hierarchy
  const headers = Object.keys(data.employees[0]);
  
  // Create header cells and append them to the header row
  headers.forEach(header => {
    const th = document.createElement('th');
    th.textContent = header;
    headerRow.appendChild(th);
  });
  
  // Append the header row to the table header
  thead.appendChild(headerRow);
  
  // Append the table header to the table
  table.appendChild(thead);
  
  // Create the table body
  const tbody = document.createElement('tbody');
  
  // Iterate through the employees array
  data.employees.forEach(employee => {
    const row = document.createElement('tr');
    
    // Iterate through the properties of each employee
    headers.forEach(header => {
      const cell = document.createElement('td');
      
      // If the property is an object, extract its values
      if (typeof employee[header] === 'object') {
        cell.textContent = Object.values(employee[header]).join(', ');
      } else {
        cell.textContent = employee[header];
      }
      
      row.appendChild(cell);
    });
    
    tbody.appendChild(row);
  });
  
  // Append the table body to the table
  table.appendChild(tbody);
  
  return table;
}

// Call the function with the data object and append the resulting table to a container element
const container = document.getElementById('tableContainer');
container.appendChild(convertObjectToTable(data));
