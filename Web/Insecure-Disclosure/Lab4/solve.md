# Lab 4 – Authentication bypass via information disclosure

## Lab Link
https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-authentication-bypass

## Description

This lab demonstrates how information disclosure can lead to authentication bypass and unauthorized access to administrative functionality.

## Solution

1. Use directory brute forcing to discover hidden endpoints.
2. The scan reveals an exposed administrative path:

/admin

3. Access the admin interface.
4. Use the discovered functionality to perform administrative actions.

## Result

The attacker deletes the user **carlos**, completing the lab objective.
