const mtMessage = "{1:F01YOURBANKAXXX0000000000}{2:I123BANKCDEFGHXXXXN}{3:{108:123456}{121:abcdef}}";

// Example: Parse the Sender's BIC
const senderBIC = mtMessage.match(/\{1:(.*?)\}/)[1];
console.log("Sender BIC:", senderBIC);

// Example: Parse the Message Type
const messageType = mtMessage.match(/\{2:(.*?)\}/)[1];
console.log("Message Type:", messageType);

// Example: Parse a specific field (e.g., Field 108)
const field108 = mtMessage.match(/\{108:(.*?)\}/)[1];
console.log("Field 108:", field108);
