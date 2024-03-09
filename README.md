const cheerio = require('cheerio');
const fs = require('fs');

// Load your HTML content
const html = fs.readFileSync('your_html_file.html');

// Load HTML into Cheerio
const $ = cheerio.load(html);

// Function to check if element has a class attribute
function hasClassAttribute(element) {
    return $(element).attr('class') !== undefined;
}

// Usage example:
$('your_selector').each((index, element) => {
    if (hasClassAttribute(element)) {
        console.log($(element).attr('class'));
    }
});
