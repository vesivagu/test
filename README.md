// Sample Swift MT message
const swiftMessage = `
{1:F01YOURBANKXAXXX0000000000}{2:I123YOURBANKXXXXN}{4:
:20:1234567890
:32A:220102USD1234567,89
:50K:/12345678901234567890
FOO BANK
123 MAIN STREET
NEW YORK, NY 10001
:59:/98765432109876543210
BAR BANK
456 PARK AVENUE
LOS ANGELES, CA 90001
-}{5:{CHK:ABC1234567890}}`;

// Define regex patterns for each field you want to extract
const regexPatterns = {
  sender: /{1:F01([^}]*)}/,
  receiver: /{2:([^}]*)}/,
  reference: /:20:([^:\n]*)/,
  amount: /:32A:([^:\n]*)/,
  beneficiary: /:50K:([^:\n]*)/,
  originator: /:59:([^:\n]*)/,
};

// Function to extract Swift MT message fields
function extractSwiftFields(message, patterns) {
  const result = {};
  for (const field in patterns) {
    const regex = patterns[field];
    const match = message.match(regex);
    if (match) {
      result[field] = match[1].trim();
    }
  }
  return result;
}

// Extract fields from the sample message
const extractedFields = extractSwiftFields(swiftMessage, regexPatterns);

// Output the extracted fields
console.log(extractedFields);
