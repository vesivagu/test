const swiftMessage = "{1:F01YOURBANKXAXXX1234567890}{2:I123BANKUS33XXXXN}{3:{108:1234567890123456}}{4:\n:20:123456789\n:32A:220801USD1234567,89\n-}";

// Define regular expressions for specific fields you want to extract
const field1Regex = /{1:([^}]+)}/;
const field2Regex = /{2:([^}]+)}/;
const field20Regex = /:20:(\d+)/;
const field32ARegex = /:32A:([A-Z]{6}\d{6}[A-Z]{3}\d+,\d+)/;

// Extract fields from the Swift message
const field1Match = swiftMessage.match(field1Regex);
const field2Match = swiftMessage.match(field2Regex);
const field20Match = swiftMessage.match(field20Regex);
const field32AMatch = swiftMessage.match(field32ARegex);

// Print extracted values
if (field1Match) {
  console.log("Field 1:", field1Match[1]);
}
if (field2Match) {
  console.log("Field 2:", field2Match[1]);
}
if (field20Match) {
  console.log("Field 20:", field20Match[1]);
}
if (field32AMatch) {
  console.log("Field 32A:", field32AMatch[1]);
}
