<!DOCTYPE html>
<html>
<head>
    <title>Upload Multiple XML Files</title>
</head>
<body>
    <h1>Upload XML Files</h1>
    <input type="file" id="fileInput" multiple>
    <button onclick="handleFiles()">Upload and Process</button>
    <div id="output"></div>

    <script>
        function handleFiles() {
            const fileInput = document.getElementById('fileInput');
            const files = fileInput.files;

            const outputDiv = document.getElementById('output');
            outputDiv.innerHTML = '';

            for (let i = 0; i < files.length; i++) {
                const file = files[i];
                if (file.type === 'text/xml') {
                    const reader = new FileReader();

                    reader.onload = function(event) {
                        const xmlString = event.target.result;
                        const parser = new DOMParser();
                        const xmlDoc = parser.parseFromString(xmlString, 'text/xml');

                        // Process the XML content as needed
                        const elements = xmlDoc.getElementsByTagName('your_tag_name'); // Replace "your_tag_name" with the tag you want to extract data from
                        for (let j = 0; j < elements.length; j++) {
                            const content = elements[j].textContent;
                            outputDiv.innerHTML += '<p>' + content + '</p>';
                        }
                    };

                    reader.readAsText(file);
                } else {
                    outputDiv.innerHTML += '<p>File ' + file.name + ' is not a valid XML file.</p>';
                }
            }
        }
    </script>
</body>
</html>
