# Crypti API

## 1. General information.

Crypti works on port 6040. All API methods have prefix: */api*. 

Like: */api/sometMethod*

API methods response format - JSON.

All responses have *status* field and *success* field. If something is wrong, response contains error field.

<table>
  <tr>
    <td>Field</td>
    <td>Description</td>
  </tr>
  <tr>
    <td>success</td>
    <td>Boolean. Result of operation. If operation is successfuly completed,  value =  true, if operation fails, value is  = false.</td>
  </tr>
  <tr>
    <td>statusCode</td>
    <td>String. Contains result operation. If operation is successfully completed, value = true, if operation fails, value =  unique error code.</td>
  </tr>
  <tr>
    <td>message</td>
    <td>String. Value =  error message.</td>
  </tr>
</table>


Crypti uses floating point arithmetic. All balances, amounts, and fees are  stored as integers. There are 8 decimal places after decimal points. Divide all values by 100000000 before displaying to user.. 

**For example:**

balance = balance / 100000000

## 2. API Methods.

### NOTE: This is only a partial list, more methods will be added in the near future.


### 2. 1. Create account.

**Url:** */api/unlock*

**Method:** *POST*

**Description: **Creates a new account, or unlocks an existing one, using the provided secret.

**Parameters:**

<table>
  <tr>
    <td>Field</td>
    <td>Description</td>
  </tr>
  <tr>
    <td>secret</td>
    <td>String. Secret phrase of account. From 1 to 100 characters.</td>
  </tr>
</table>


**Response:**

<table>
  <tr>
    <td>Field</td>
    <td>Description</td>
  </tr>
  <tr>
    <td>success</td>
    <td>Boolean. Result of success of operation.</td>
  </tr>
  <tr>
    <td>status</td>
    <td>String. "OK" or unique error code.</td>
  </tr>
  <tr>
    <td>secondPassphrase</td>
    <td>Boolean. true if account working with second passphrase, false if account doesn’t have second passphrase.</td>
  </tr>
  <tr>
    <td>address</td>
    <td>String. Address of account.</td>
  </tr>
  <tr>
    <td>publicKey</td>
    <td>String. Public key of account converted to hex format.</td>
  </tr>
  <tr>
    <td>balance</td>
    <td>Integer. Total balance of account, after all required confirmations.</td>
  </tr>
  <tr>
    <td>unconfirmedBalance</td>
    <td>Integer. The unconfirmed balance of account, pending the required confirmations.</td>
  </tr>
  <tr>
    <td>effectiveBalance</td>
    <td>Integer. Balance confirmed by 1440 blocks (around 24 hours). </td>
  </tr>
</table>


### 2. 2. Get balance.

**Url:** */api/getBalance*

**Method**: *GET*

**Description***: Return balance of current address/account.*

**Parameters**:

<table>
  <tr>
    <td>Field</td>
    <td>Description</td>
  </tr>
  <tr>
    <td>address</td>
    <td>String. Address of account</td>
  </tr>
</table>


**Response:**

<table>
  <tr>
    <td>Field</td>
    <td>Description</td>
  </tr>
  <tr>
    <td>success</td>
    <td>Boolean. Result of success of operation.</td>
  </tr>
  <tr>
    <td>status</td>
    <td>String. "OK" or unique error code.</td>
  </tr>
  <tr>
    <td>secondPassphrase</td>
    <td>Boolean. true if account working with second passphrase, false if account doesn’t have second passphrase.</td>
  </tr>
  <tr>
    <td>balance</td>
    <td>Integer. Total confirmed balance of account. </td>
  </tr>
  <tr>
    <td>unconfirmedBalance</td>
    <td>Integer. Unconfirmed balance of account. </td>
  </tr>
  <tr>
    <td>effectiveBalance</td>
    <td>Integer. Balance confirmed by 1440 blocks (around 24 hours). </td>
  </tr>
</table>


### 2. 3. Send Crypti.

**Url:** */api/sendFunds*

**Method:** *POST*

**Description:** Send Crypti to another account. Fee will be calculated and applied automatically.

**Parameters**: 

<table>
  <tr>
    <td>Field</td>
    <td>Description</td>
  </tr>
  <tr>
    <td>secret</td>
    <td>String. SecretPhrase of sender account.</td>
  </tr>
  <tr>
    <td>amount</td>
    <td>Float. Amount to be sent.</td>
  </tr>
  <tr>
    <td>recipient</td>
    <td>String. Recipient address.</td>
  </tr>
  <tr>
    <td>accountAddress</td>
    <td>String. Send account address. Use only if you want to validate your secretPhrase before send. Optional.</td>
  </tr>
  <tr>
    <td>secondPhrase</td>
    <td>String. Second signature of account. Use only if you added second signature and this signature is confirmed. Optional.</td>
  </tr>
</table>


**Response:**

<table>
  <tr>
    <td>Field</td>
    <td>Description</td>
  </tr>
  <tr>
    <td>success</td>
    <td>Boolean. Result of success of operation.</td>
  </tr>
  <tr>
    <td>status</td>
    <td>String. "OK" or unique error code.</td>
  </tr>
  <tr>
    <td>transactions</td>
    <td>Array. JSON array of transactions.</td>
  </tr>
</table>


### 2. 4. Network fee.

**Url:** */api/getFee*

**Method**: *GET*

**Description: **Return current transaction fee in percent from Crypti network. It’s using to show user how much fee he spend in transaction.

**Parameters**: nothing.

**Response:**

<table>
  <tr>
    <td>Field</td>
    <td>Description</td>
  </tr>
  <tr>
    <td>success</td>
    <td>Boolean. Result of method work.</td>
  </tr>
  <tr>
    <td>status</td>
    <td>String. "OK" or unique error ID.</td>
  </tr>
  <tr>
    <td>fee</td>
    <td>Float. Current fee of network, in percent.</td>
  </tr>
</table>


### 2. 5. Transactions List.

**Url:** */api/getAddressTransactions*

**Method**: *GET*

**Description: **Return last N transactions for the provided address.

**Parameters**: 

<table>
  <tr>
    <td>Field</td>
    <td>Description</td>
  </tr>
  <tr>
    <td>address</td>
    <td>String. Address of transactions (sender, recipient).</td>
  </tr>
  <tr>
    <td>limit</td>
    <td>Integer. Limit of transactions. Optional parameter. Default value: 100.</td>
  </tr>
  <tr>
    <td>descOrder</td>
    <td>Boolean. Descending (true) or ascending (false) ordering, according to the transaction timestamps. Optional parameter. Default value: ascending(false)</td>
  </tr>
</table>


**Response:**

<table>
  <tr>
    <td>Field</td>
    <td>Description</td>
  </tr>
  <tr>
    <td>success</td>
    <td>Boolean. Result of success of operation.</td>
  </tr>
  <tr>
    <td>status</td>
    <td>String. "OK" or unique error code.</td>
  </tr>
  <tr>
    <td>transactions</td>
    <td>Array. JSON array of transactions.</td>
  </tr>
</table>


**Example of transaction: **

{
      "id": "10345457625055490607",
      "blockId": "1114347129191230720",
      "type": 0,
      "subtype": 0,
      "timestamp": 1407292194,
      "senderPublicKey": "9e51284be9f60a367d57b8d9dc40fb7a1e95cdf9c4ba249f4e96809fa05d5982",
      "sender": "3364313429379719464C",
      "recipient": "6881298120989278452C",
      "amount": 1000000000000,
      "fee": 10000000000,
      "signature": "980e7f3c3bec4c49e82a0563f5e273a1a737b497c5df1e387616ada9121cfe2d81a86ad6fcdb9cfb6bddae17313669bba8fbf442138b5d789c701c905cd89a0f",
      "signSignature": null,
      "confirmations": 15,
      "confirmed": true
},

**Unconfirmed transaction:**

{
      "type": 0,
      "subtype": 0,
      "id": "18328062892813578757",
      "timestamp": 1407293940,
      "senderPublicKey": "808c2a6e3bf0a8a6edd64356e98c8aab4daeacb4dc177a8a20a6442b40d1f0e0",
      "recipientId": "3364313429379719464C",
      "amount": 10000000000,
      "fee": 100000000,
      "signature": "69c08c21e8466aca5ed5573ceb5b99af576324342c02a2ba7c7c867931c0acd68f35036663715a16159d52bbf14a9b7176ba4ded5e4d7c9ba4ef173a53e6bc04",
      "height": 0,
      "asset": null,
      "sender": "6881298120989278452C",
      "confirmations": "-",
      "recipient": "3364313429379719464C",
      "confirmed": false
},


### 2. 6. Get specific transaction details

**Url:** */api/getTransaction?transactionId=TXT_ID*

**Method**: *GET*

**Description: **Return the details of the transaction specified by the transaction id.

**Parameters**: 

<table>
  <tr>
    <td>Field</td>
    <td>Description</td>
  </tr>
  <tr>
    <td>transaction ID</td>
    <td>String. ID of the transaction</td>
  </tr>
</table>


**Response:**

<table>
  <tr>
    <td>Field</td>
    <td>Description</td>
  </tr>
  <tr>
    <td>success</td>
    <td>Boolean. Result of success of operation.</td>
  </tr>
  <tr>
    <td>status</td>
    <td>String. "OK" or unique error code.</td>
  </tr>
  <tr>
    <td>transaction</td>
    <td>Array. JSON array of transactions.</td>
  </tr>
</table>


**Example of transaction: **

{
      "id": "10345457625055490607",
      "blockId": "1114347129191230720",
      "type": 0,
      "subtype": 0,
      "timestamp": 1407292194,
      "senderPublicKey": "9e51284be9f60a367d57b8d9dc40fb7a1e95cdf9c4ba249f4e96809fa05d5982",
      "sender": "3364313429379719464C",
      "recipient": "6881298120989278452C",
      "amount": 1000000000000,
      "fee": 10000000000,
      "signature": "980e7f3c3bec4c49e82a0563f5e273a1a737b497c5df1e387616ada9121cfe2d81a86ad6fcdb9cfb6bddae17313669bba8fbf442138b5d789c701c905cd89a0f",
      "signSignature": null,
      "confirmations": 15,
      "confirmed": true
},
