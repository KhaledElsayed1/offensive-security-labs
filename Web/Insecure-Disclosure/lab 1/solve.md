# Lab 1 – Information disclosure in error messages

## Lab Link
https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-in-error-messages

## Description

This lab demonstrates how detailed error messages can expose sensitive internal information about the application.

## Solution

1. Open any product page in the application.
2. Notice that the page uses the parameter:
/product?productId=1

3. Intercept the request using Burp Suite and send it to Repeater.
4. Modify the parameter value to an invalid value.

Example:
/product?productId=test

5. The server returns an error message revealing the framework version used by the application.

## Result

The exposed framework version is submitted in the solution field to solve the lab.

