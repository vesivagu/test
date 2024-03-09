const cheerio = require('cheerio');

// Sample HTML content
const htmlContent = `
<div>
  <div>
    <p class="paragraph">This is a paragraph.</p>
  </div>
  <div>
    <p>This is another paragraph.</p>
  </div>
</div>
`;

// Load HTML content using cheerio
const $ = cheerio.load(htmlContent);

// Specify the parent element where you want to search
const parentElement = $('div');

// Iterate over child elements of the parent element
parentElement.children().each((index, element) => {
  const childElement = $(element);

  // Check if the element has a class attribute
  if (childElement.attr('class')) {
    console.log('Element has a class attribute:', childElement.text());
  }
});
