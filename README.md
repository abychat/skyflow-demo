# Skyflow Elements - Collect and Reveal Vault Data

## Introduction

This section of the workshop will walk you through the process of using Skyflow Elements to collect and reveal vault data.


Skyflow Elements provides a secure way to collect and reveal sensitive data, such as personally identifiable information (PII) and credit card information (PCI). It offers several benefits, including complete programmatic isolation from your frontend applications, end-to-end encryption, tokenization, and the ability to customize the look and feel of the data collection form.

  
In this guide, we will explore how you can integrate Skyflow Elements into existing applications and workflows by leveraging Skyflow SDKs with your Skyflow credentials, and using the client-side SDK to create and customize a data collection form.

## Prerequisites

  

-   A Quickstart vault that you created in the previous exercises.
    
-   VAULT_ID, VAULT_URL for the. You can obtain these by clicking the vault menu icon > Edit vault details.Note your Vault URL and Vault ID values, then click Cancel.
    
-   Ability to execute shell scripts and install the following on a Command Prompt or Terminal:
    

    -   [Node.js](https://nodejs.org/en/) version 10 or above
    

    -   Note: For Windows Machines we recommend having the [Windows Subsystem for Linux (WSL2](https://learn.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-wsl#install-wsl-2)) and [Windows Terminal](https://learn.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-wsl#install-windows-terminal-optional) installed
    

    -   [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) version 6.x.x
    
    -   [Express.js](http://expressjs.com/en/starter/hello-world.html)
    

## Create a service account

1.  In Studio, click Settings in the upper navigation.
    
2.  In the side navigation, click Vault, then choose the Quickstart vault from the dropdown menu.
    
3.  Click on IAM on the side navigation, and then click on Service Accounts > New Service Account.
    
4.  For Name, enter "Workshop Integration". For Roles, choose Vault Owner.
    
5.  Click Create.
    
6.  Your browser downloads a credentials.json file. Store this file in a secure location. You'll need it to generate bearer tokens.
    

## Setup Bearer Token Generation Endpoint

  

We will now set up a Node.js based backend service that will generate a bearer token. This service will be invoked by the front-end to obtain a bearer token to authenticate and use the Skyflow API.

  

The first step is to install all the Node.js libraries required for running the endpoint. Based on your preference, you could choose to follow either of the following options:

  

### Node.JS Project Setup

  

1.  Open Command Prompt on Windows or Terminal on Mac, navigate to your preferred directory and create a new directory named bearer-token-generator.
    
```
mkdir  bearer-token-generator
```
2.  Navigate to bearer-token-generator directory.
```    
cd  bearer-token-generator
```
3.  Initialize npm
```    
npm  init --yes
```
4.  Install skyflow-node
```    
npm  i  skyflow-node
```
5.  Install express
```    
npm  i  express
```
6.  Install cors
```    
npm  i  cors
```
7.  Install live-server.
```    
npm  install  -g  live-server
```
8.  Copy the creds.json file that you downloaded in the [Create a service account](https://docs.skyflow.com/api-authentication/#create-a-service-account) section to the bearer-token-generator directory.
    
9.  Copy the index.js from the folder you downloaded from Github to the bearer-token-generator directory.
    
10.  Run the following command to start your local server.
```    
node  index.js
```
11.  The server will start at localhost:3000. Your <TOKEN_END_POINT_URL> for subsequent sections would be http://localhost:3000/
    

## Configure the HTML file

Next we will configure the HTML file and supply the vault details needed to invoke the bearer token generation endpoint. This code lever
  

1.  Navigate to the folder you downloaded from Github.
    
2.  Open the form.html file in your preferred editor or IDE.
    
3.  The code in form.html does the following:
    

-   Defines HTML elements to mount elements onto.
    
-   Initializes the SDK with your vault's values, including fetching a bearer token from the server-side SDK.
    
-   Defines a collect container and the elements it contains.
    
-   Mounts the collect container onto the HTML element.
    
-   Defines the reveal elements.Mounts the reveal elements onto the HTML element.
    
-   Configures the Collect PCI Data button to collect data from the collect container and update the reveal element with the token.
    
-   Configures the Reveal button to reveal the data in the reveal element.
    

4.  Replace <VAULT_ID> and <VAULT URL> with your vault-specific values.
    
5.  Replace <TOKEN_END_POINT_URL> with  [http://localhost:3000/](http://localhost:3000/)
    

### Load the HTML File in the browser

Issue the following command from the Terminal to load the HTML page:
```
npx  live-server  form.html  --port=8000
```
  
You should see the form.html load in your browser.

  
## Experience Skyflow Elements


1.  Your forms.html page should allow you to input Name, SSN, Phone, Email and DOB. Submitting the data should result in a new record being created in the Vault too.
  
2.  Enter data in each column.
  
3.  Click on the Collect PII Data button. You will see the API response as well as the Reveal Elements section along with the Reveal PCI Data button appear on the page.
  
4.  Scroll down to the bottom of the page and click on Reveal PCI Data to view detokenized data.
