// Install the swift-mt-parse library
npm install swift-mt-parse

// Import the library into your JavaScript code
const swiftMTParse = require('swift-mt-parse');

// Define your Swift MT message
const mtMessage = `
{1:F01YOURBANKXAXXX0000000000}{2:O1031609050915YOURBANKXAXXX00000000000509151039N}{3:{108:MT103 007 OF 010}{121:5f94a52c-f0d9-4bb9-a9e3-38f92823f8bf}}{4:
:20:REFERENCE
:23B:CRED
:32A:220823USD2500,
:50K:/12345678901234567890
:59:/98765432109876543210
:71A:OUR
-}
`;

// Parse the Swift MT message
const parsedMessage = swiftMTParse(mtMessage);

// Access specific fields or information
console.log(parsedMessage.fields[20]); // Access the value of field 20
