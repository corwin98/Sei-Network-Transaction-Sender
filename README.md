# Sei-Network-Transaction-Sender
This script allows you to send SEI tokens from one account to another on the Sei Network. It utilizes the sei-sdk package to connect to the network and send transactions.
const { SeiSDK } = require('sei-sdk');

async function sendTokens(fromAddress, toAddress, amount) {
  // Connect to the Sei Network
  const sdk = await SeiSDK.connect();

  // Retrieve the account from which to send tokens
  const fromAccount = await sdk.accounts.get(fromAddress);

  // Create a transaction to send tokens
  const transaction = sdk.transactions.createTransferTransaction(
    fromAccount,
    toAddress,
    amount
  );

  // Sign and send the transaction
  const signedTransaction = await sdk.transactions.signTransaction(
    transaction,
    fromAccount
  );
  const result = await sdk.transactions.send(signedTransaction);

  // Display the transaction result
  console.log('Transaction Result:', result);
}

// Usage example
const fromAddress = '0x...'; // Specify the sender's address
const toAddress = '0x...'; // Specify the recipient's address
const amount = 100; // Specify the amount of SEI tokens to send

sendTokens(fromAddress, toAddress, amount);
