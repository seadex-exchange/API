# Start Guide

## SEADEX API Overview

Seadex provides users with a simple but powerful API service designed to help users to quickly and efficiently integrate the trading functions of Seadex (Seadex.io)  into their own applications.

## With our API, you can quickly implement the following features

- Latest Market Conditions

- Trading Information

- Account Information

- Depth Information of Buyers and Sellers

- Order Information

- Quick Buy and Sell

- Order Cancellations

All requests are based on the `http` protocol. The `contentType` in the request header information needs to be uniformly set to: `'application/x-www-form-urlencoded'`, access root URL: `http://api.seadex.io/`

For example：

```
contentType:'application/x-www-form-urlencoded'
```

If you have any problems during use, please contact our technical discussion telegram group: Seadex official API technology exchange group: 325248096, we will make the most authoritative answers for you.

## Getting Started

Seadex provides users with a simple but powerful API service designed to help users to quickly and efficiently integrate the trading functions of Seadex (Seadex.io)  into their own applications.

### REST API

REST, or Representational State Transfer, is currently the most popular Internet software architecture. It is well-structured, standards-compliant, easy to understand, and easy to expand. It is being adopted by more and more websites. The advantages are as follows:

- In the RESTful architecture, each URL represents a resource; 

- Between the client and the server, a certain presentation layer of such resources is passed; 

- The client operates on the server-side resources through four HTTP instructions to implement the "presentation layer state  Conversion".

**Developers are advised to use the REST API for currency transactions or asset withdrawals.**

### WebSocket API 

Seadex also provides users with a fast and efficient API for WebSocket.

WebSocket is a new protocol for HTML5. It implements full-duplex communication between the client and the server, enabling data to travel in both directions quickly. The client and server connections can be established through a simple handshake, and the server can actively push information to the client according to business rules. The advantages are as follows:

- When the client and the server perform data transmission, the request header information is relatively small, about 2 bytes; 

- Both the client and the server can actively send data to the other party; 

- There is no need to create TCP requests and destruction for multiple times, saving bandwidth and server resources. 

**Developers are strongly encouraged to use the WebSocket API to obtain information such as market conditions and trading depth.**

## Enable API Permission    

The user's API permissions can be obtained from the site's Security->API. Click on the “Apply for API” to get it. The apiKey is the access key that Seadex provides to the API user, and secretKey is the private key used to sign the request parameter.

**Notice: Do not reveal these two parameters to anyone. These two parameters are related to the security of your account.**

## Generate a string to be signed 

The parameters submitted by the user must participate in the signature except for the sign. The character string to be signed needs to be sorted according to the parameter name (firstly compare the first letter of all parameter names, arranged in order of abcd, if you encounter the same initial letter, look at the second letter, and so on.)

For example: sign the following parameters
```
string[] parameters={  
  "api_key=c821db84-6fbd-11e4-a9e3-c86000d26d7c"，  
  "symbol=eth_btc",  
  "type=buy",  
  "price=680",  
  "amount=1.0"  
}; 
```

Generate the character string to be signed as:

```
amount=1.0&api_key=c821db84-6fbd-11e4-a9e3-c86000d26d7c&price=680&symbol=eth_btc&type=buy.
```

## MD5 Signature

When signing MD5, it is necessary to use secretKey. Add the private key parameter to the character string to be signed to generate the final signature string, for example: 

```
amount=1.0&api_key=c821db84-6fbd-11e4-a9e3-c86000d26d7c&price=680&symbol=eth_btc&type=buy&secret_key=secretKey 
```

**Notice: `&secret_key=secretKey` is the necessary parameter for signing.**

It is used to perform the signature operation on the final string to be signed, thereby obtaining the signature result string (the string is assigned to the parameter sign), and the letters in the MD5 calculation result are all uppercase.



## Request Interaction Description

1. Request parameters: packaging parameter according to API request parameters.

2. Submit request parameters: submit the request parameter package to server via `POST` or `GET`.

3. Server response: firstly, the server will perform parameter security verification on the user request data, and returns the response data to the user in JSON format according to the business logic after verification.

4. Data processing: Processing server response data.

