<!DOCTYPE html>
<html>
<head>
    <title>Print Selected Rows to PDF</title>
</head>
<body>
    <table id="data-table">
        <!-- Your table headers -->
        <tr>
            <th>Select</th>
            <th>Column 1</th>
            <th>Column 2</th>
            <!-- Add more column headers as needed -->
        </tr>
        <!-- Your table rows and data go here -->
        <tr>
            <td><input type="checkbox"></td>
            <td>Data 1</td>
            <td>Data 2</td>
            <!-- Add more data cells as needed -->
        </tr>
        <!-- Add more rows as needed -->
    </table>
    <button id="print-pdf">Print Selected Rows to PDF</button>

    <!-- Include JavaScript libraries -->
    <!-- For example, you can use jsPDF to create a PDF on the client-side -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.4.0/jspdf.umd.min.js"></script>
    <script src="your-custom-script.js"></script>
</body>
</html>




// Wait for the document to be fully loaded
document.addEventListener("DOMContentLoaded", function () {
  // Get the table element
  const table = document.getElementById("data-table");

  // Get the button to print the PDF
  const printButton = document.getElementById("print-pdf");

  // Function to generate PDF from selected rows
  function generatePDF() {
    // Create a new jsPDF instance
    const doc = new jsPDF();

    // Set the initial y-position for content
    let y = 20;

    // Loop through the table rows
    for (let i = 1; i < table.rows.length; i++) {
      // Check if the checkbox is checked
      if (table.rows[i].cells[0].querySelector("input").checked) {
        // Get the row data and add it to the PDF
        const rowData = Array.from(table.rows[i].cells).map((cell) => cell.innerText);
        doc.text(20, y, rowData.join(", "));
        y += 10;
      }
    }

    // Save the PDF
    doc.save("selected_rows.pdf");
  }

  // Attach click event to the "Print PDF" button
  printButton.addEventListener("click", generatePDF);
});

