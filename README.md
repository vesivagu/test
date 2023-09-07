// Sample Swift MT message
var swiftMessage = "{1:F01BANKUS33AXXX1234567890}{2:O1031609050901BANKUS33AXXX12345678900509010501N}{4:\n:20:REFERENCE\n:32A:210901USD12345,67\n-}";

// Function to extract a specific field by its field tag
function extractField(message, fieldTag) {
    var tagStart = message.indexOf(":" + fieldTag + ":");
    if (tagStart !== -1) {
        var tagEnd = message.indexOf("\n", tagStart);
        if (tagEnd !== -1) {
            return message.substring(tagStart + fieldTag.length + 2, tagEnd);
        }
    }
    return null;
}

// Extract the 20 (Reference) field
var referenceField = extractField(swiftMessage, "20");
console.log("Reference Field: " + referenceField);

// Extract the 32A (Amount) field
var amountField = extractField(swiftMessage, "32A");
console.log("Amount Field: " + amountField);
