# Lab 5 – Information disclosure in version control history

## Lab Link
https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-in-version-control-history

## Description

This lab demonstrates how exposed version control repositories can leak sensitive information through commit history.

## Solution

1. Perform directory enumeration to discover hidden files.
2. A `.git` directory is discovered on the server.
3. Download the repository using tools such as wget.
4. Inspect the repository and analyze commit history.
5. Old commits reveal administrator credentials that were previously removed.

## Result

Using the discovered credentials, log in as the administrator and delete the user **carlos** to solve the lab.
