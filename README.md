const cheerio = require('cheerio');
const fs = require('fs');

// Load your HTML file
const html = fs.readFileSync('path/to/your/file.html', 'utf8');

// Load HTML into Cheerio
const $ = cheerio.load(html);

// Function to check if element has a class attribute
function hasClassAttribute(element) {
  return element.attribs && element.attribs.class;
}

// Find all elements in the HTML with class attribute
const elementsWithClass = $('*').filter((index, element) => hasClassAttribute(element));

// Log the elements with class attribute
elementsWithClass.each((index, element) => {
  console.log(element.name, element.attribs.class);
});
