// Sample Swift MT message
const swiftMTMessage = "{1:F01YOURBANKAXXX0000000000}{2:O1031234150923YOURBANKAXXX00000000001509231509N}";

// Tokenize the message by curly braces
const tokens = swiftMTMessage.split(/({\d+:)|(:\d+})/).filter(Boolean);

// Parse the tokens
const parsedMessage = {};
for (let i = 0; i < tokens.length; i += 2) {
  const fieldTag = tokens[i];
  const fieldValue = tokens[i + 1];
  parsedMessage[fieldTag] = fieldValue;
}

console.log(parsedMessage);
