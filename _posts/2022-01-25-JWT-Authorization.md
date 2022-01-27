---
title: "JWT Authorization"
date: 2022-01-25
---

What is JWT and for what purpose it is used? 
JWT provides a way to communicate securely between 2 parties. It is used for the following purposes 
1. Authorization - Once the user is logged in, the JWT token is used for all subsequent interactions, allowing the user to access resources that are permitted with their token. It's a lightweight protocol and in all single sign-on features use this mechanism. 
2. Securely exchange information - Since JWT supports public/private key pairs. The receiver can verify its authenticity using the public key.


Structure of JWT
A typical JWT looks like - xxxxx.yyyyy.zzzzz


The JWT is composed of 3 parts encoded in BASE64 and separated by '.'. 


1. Header - This portion tells us how the JWT is being signed. The header contains 2 parts: the type of the token, which is JWT, and the signing algorithm being used, such as HMAC SHA256 or RSA.
2. Payload - This part contains the data that we need to uniquely identify and authorize a user.
3. Signature - This part is calcualtes by encoding Header & payload with a secret key. Only server can validate the signature as it has the secret key. JWT can never be tempored as signature is calculated using header and the data portion.


Drawbacks of JWT
1. You can save sensitive information like user name, DOB, password. As payload is not encrypted and is visible to all.
2. If someone has stolen user JWT then we can't invlidate it. Server will need to maintain in-memory list of revoked JWT's

