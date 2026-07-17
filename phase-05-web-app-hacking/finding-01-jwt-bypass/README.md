# Finding 01 — JWT Signature Verification Bypass

## Severity
Critical

## Vulnerability
JWT Signature Verification Bypass — Privilege Escalation to Admin

## Description
The application issues JSON Web Tokens (JWT) upon user 
authentication, storing the user's role as a claim within 
the token payload. The server does not verify the JWT 
signature before trusting the claims contained within the 
token. By modifying the is_admin claim from false to true, 
a low-privileged user was able to gain full administrative 
access to the admin panel at /sup3r_s3cr3t_admin.

## Steps to Reproduce
1. Perform passive reconnaissance using WHOIS, dig, 
   nslookup, WhatWeb, and curl -I
2. Register a regular user account at /register
3. Intercept the login response in Burp Suite and 
   extract the JWT token
4. In Burp Repeater, use JWT Editor to modify 
   is_admin from false to true
5. Send request to GET /sup3r_s3cr3t_admin
6. Observe 200 OK response with full admin panel access

## Impact
An attacker can access the admin panel and perform the 
following: view and export 8000+ user records, approve 
fraudulent loans, delete or suspend accounts, and create 
new administrator accounts. This is a critical breach of 
Confidentiality and Integrity in the CIA triad.

## Recommendation
- Enforce JWT signature verification on every request
- Use a strong cryptographically random secret key 
  of at least 256 bits
- Implement short token expiry (15-60 minutes)
- Store role information server-side and look up from 
  database rather than trusting token claims

## Evidence
Screenshots located in /screenshots folder
