# Lab 3 – Information disclosure via backup files

## Lab Link
https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-via-backup-files

## Description

This lab demonstrates how backup files left on the server can expose application source code.

## Solution

1. Explore the application directories.
2. Look for files with backup extensions such as:

.bak  
.old  
.backup

3. A backup file containing source code is discovered.
4. Open the file and analyze its contents.

## Result

Sensitive information such as administrator credentials is found inside the source code and submitted to solve the lab.
