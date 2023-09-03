// Sample Swift MT message string
const swiftMessage = `
    {1:F01YOURBANKXAXXX0000000000}{2:I103YOURBANKXXXXXN}{3:{108:1234567890123456}}{4:
    :20:REFERENCE
    :23B:CRED
    :32A:220117USD1234567,89
    :33B:USD1234567,89
    :50A:/1234567890
    :59:/9876543210
    -}`;

// Define a regular expression pattern to match Swift MT messages
const mtMessagePattern = /\{1:[^\}]+\}/g;

// Extract Swift MT messages from the input string
const extractedMessages = swiftMessage.match(mtMessagePattern);

// Output the extracted messages
for (const message of extractedMessages) {
    console.log("Extracted MT Message:");
    console.log(message);
}
