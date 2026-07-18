Severity: Medium
Description: The application does not set four critical HTTP security headers in its responses. The missing headers are: X-Frame-Options, X-Content-Type-Options, Content-Security-Policy, and Strict-Transport-Security. These headers instruct browsers to enforce security controls that protect users from common web attacks.
Impact: The absence of these headers exposes users to the following attacks — Clickjacking via iframe embedding, MIME sniffing attacks through unvalidated content types, Cross-Site Scripting via unrestricted script sources, and SSL stripping attacks that downgrade HTTPS connections to HTTP.
Recommendation: Add the following headers to all server responses:
X-Frame-Options: DENY
X-Content-Type-Options: nosniff
Content-Security-Policy: default-src 'self'
Strict-Transport-Security: max-age=31536000; includeSubDomains
