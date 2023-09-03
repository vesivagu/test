// Sample Swift MT message (MT103)
const swiftMessage = `
    {1:F01YOURBANKAXXX0000000000}{2:I103BANKBICXXXXXN}{4:
    :20:REFERENCE_NUMBER
    :23B:CRED
    :32A:210101USD1234567,89
    :50K:/1234567890
    YOUR CUSTOMER NAME
    ADDRESS LINE 1
    ADDRESS LINE 2
    :59:/9876543210
    RECEIVER NAME
    RECEIVER ADDRESS LINE 1
    RECEIVER ADDRESS LINE 2
    -}
`;

// Custom parsing function (simplified)
function parseSwiftMT103(swiftMessage) {
    const parsedData = {
        sender: swiftMessage.match(/:50K:(.*?)\n/)[1],
        receiver: swiftMessage.match(/:59:(.*?)\n/)[1],
        reference: swiftMessage.match(/:20:(.*?)\n/)[1],
        // Add more fields as needed
    };
    return parsedData;
}

// Parse the Swift MT message
const parsedData = parseSwiftMT103(swiftMessage);

// Output the parsed data
console.log(parsedData);
