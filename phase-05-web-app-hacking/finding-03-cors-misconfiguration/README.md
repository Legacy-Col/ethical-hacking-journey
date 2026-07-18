Severity: High

Description: The application sets Access-Control-Allow-Origin: * in all HTTP responses, allowing any external website to make cross-origin requests to VulnBank's API. This wildcard configuration means no origin restriction is enforced on API endpoints.
Impact: An attacker can create a malicious website that silently makes authenticated API requests to VulnBank on behalf of a logged-in victim. In a banking context this could result in unauthorized account balance enumeration, fraudulent money transfers, and theft of personal financial data — all without the victim's knowledge.
Recommendation: Replace the wildcard with explicitly trusted origins:
Access-Control-Allow-Origin: https://vulnbank.org
Never use wildcard CORS on authenticated endpoints, especially those handling financial transactions.
