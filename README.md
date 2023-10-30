# Guide to Integrating Immutable Passport into Your Application
## Introduction:
Immutable Passport is a powerful authentication solution that allows users to securely log in and access various features of your application. This guide will walk you through the step-by-step process of integrating Immutable Passport into your application. By the end of this guide, you will be able to authenticate users, display user information, and initiate transactions through Passport.
## Prerequisites:
- Basic knowledge of JavaScript and Node.js
- Understanding of API calls and OAuth2 authentication

### Step 1: Setting up a Simple Application
To start integrating Immutable Passport, create a simple application or clone an existing repository of a simple application that you want to integrate with Passport. This will serve as the basis for the integration process.

### Step 2: Registering the Application on Immutable Developer Hub
- Go to the Immutable Developer Hub website (https://developer.immutable.com/) and create an account if you haven't already.
- Once logged in, navigate to the "Applications" section and click on "Create Application".
- Fill in the required information, including the application name and the authorization callback URL.
- After registering, you will receive a client ID and a client secret. These will be used in the next steps of the integration process.

### Step 3: Installing and Initializing the Passport Client
- Install the Immutable Passport client package by running the following command in your application's directory:
   
   npm install @imtbl/passport
   
- Initialize the Passport client in your application by configuring it with the client ID and client secret obtained from the Immutable Developer Hub. The following code snippet demonstrates this setup:
   javascript
   const { Passport } = require('@imtbl/passport');

   const passport = new Passport({
     clientID: 'YOUR_CLIENT_ID',
     clientSecret: 'YOUR_CLIENT_SECRET',
   });

   // Additional configuration and setup can be done here
   

### Step 4: Logging in a User with Passport
- Create a login button or link in your application's user interface that triggers the authentication process.
- On click, redirect the user to the Passport authorization URL, passing the necessary parameters like the scope and state.
   javascript
   const loginButton = document.getElementById('login-button');
   loginButton.addEventListener('click', () => {
     passport.login({ scope: 'openid profile' });
   });
   
- Once the user successfully logs in and grants the requested permissions, they will be redirected back to the provided authorization callback URL.
- Extract the authorization code from the URL and exchange it for an access token and an ID token using the Passport client.
   javascript
   const authorizationCode = extractAuthorizationCodeFromURL();

   passport.getToken(authorizationCode)
     .then((tokens) => {
       // Store the tokens securely or use them as required
     })
     .catch((error) => {
       // Handle token retrieval error
     });
   

### Step 5: Displaying User Information
- After obtaining the tokens, you can use the ID token to fetch user details.
   javascript
   passport.getUserInfo()
     .then((userInfo) => {
       // Extract necessary user information like nickname
       const { nickname } = userInfo;
       // Display user's nickname in your application UI
     })
     .catch((error) => {
       // Handle user information retrieval error
     });
   
_ You can also display the ID token and access token obtained from Passport, providing transparency to the user.

### Step 6: Logging out a User
- Create a logout button or link that triggers the user logout process.
   javascript
   const logoutButton = document.getElementById('logout-button');
   logoutButton.addEventListener('click', () => {
     passport.logout();
   });
   
- Upon clicking the logout button, the user will be redirected to the Immutable logout page, and their session will be terminated.

### Step 7: Initiating a Transaction from Passport
- To initiate a transaction from Passport, you can use the Passport client's `transaction` method.
   javascript
   const transactionHash = await passport.transaction('placeholder string');
   // Use the transaction hash as required
   

## Conclusion:
By following the steps outlined in this guide, you have successfully integrated Immutable Passport into your application. Users can now securely authenticate, view user information, initiate transactions, and more using the power of Immutable Passport. Happy coding!
