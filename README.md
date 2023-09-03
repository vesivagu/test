// Sample Swift MT message (MT103)
const swiftMessage = `
{1:F01BANKUS33AXXX0000000000}{2:I103BANKUS33XXXXN}{4:
:20:1234567890
:23B:CRED
:32A:220825USD12345,67
:50K:/1234567890
JOHN DOE
123 MAIN STREET
NEW YORK, NY 10001
:52A:BANKUS33
:53A:BANKUS33
:54A:/5678901234
XYZ BANK
567 WALL STREET
LOS ANGELES, CA 90001
:57A:/9876543210
BENEFICIARY CORP
987 HIGHWAY ROAD
SAN FRANCISCO, CA 90002
-}
`;

// Define a function to parse Swift MT messages
function parseSwiftMT(swiftMessage) {
  const fields = swiftMessage.match(/:[0-9A-Z]{2,}:[^\r\n]*(?=\r?\n|$)/g);

  if (fields) {
    const parsedData = {};
    fields.forEach((field) => {
      const parts = field.split(':');
      const tag = parts[1];
      const value = parts[2];
      parsedData[tag] = value.trim();
    });
    return parsedData;
  } else {
    return null; // Invalid or unsupported format
  }
}

// Parse the Swift MT message
const parsedSwiftMT = parseSwiftMT(swiftMessage);

// Output the parsed data
console.log(parsedSwiftMT);
