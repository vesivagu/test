// Sample Swift MT message
const swiftMTMessage = "{1:F01YOURBANKXAXXX0000000000}{2:O1031234170906YOURBANKXXXX00000000001709060934N}{3:{103:TGT}{108:1234567890123456}}";

// Define the field codes you want to extract
const fieldCodes = ["20", "32A", "58A"];

// Function to extract fields from the message
function extractFields(message, fieldCodes) {
  const extractedFields = {};

  for (const code of fieldCodes) {
    const regex = new RegExp(`{${code}:([^{}]+)}`);
    const match = regex.exec(message);
    if (match) {
      extractedFields[code] = match[1];
    }
  }

  return extractedFields;
}

const extractedData = extractFields(swiftMTMessage, fieldCodes);
console.log(extractedData);
