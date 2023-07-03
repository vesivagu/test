function convertComplexObjectToTable(object) {
  let html = '<table>';

  // Recursive function to process nested properties
  function processObject(obj, parentKey = '') {
    for (let key in obj) {
      if (obj.hasOwnProperty(key)) {
        let value = obj[key];
        let currentKey = parentKey ? parentKey + '.' + key : key;
        
        if (typeof value === 'object' && !Array.isArray(value)) {
          // Process nested object recursively
          processObject(value, currentKey);
        } else {
          // Create table row
          html += '<tr>';
          html += '<td>' + currentKey + '</td>';
          html += '<td>' + value + '</td>';
          html += '</tr>';
        }
      }
    }
  }

  // Call the recursive function to generate table rows
  processObject(object);

  html += '</table>';

  return html;
}
