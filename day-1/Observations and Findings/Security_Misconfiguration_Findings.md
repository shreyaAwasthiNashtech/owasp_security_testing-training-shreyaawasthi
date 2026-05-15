Security Misconfiguration Findings:

Vulnerability Category:
OWASP Top 10 – A05:2021 Security Misconfiguration


Introduction:
During testing of OWASP Juice Shop, several security configuration weaknesses were identified. These issues included missing or outdated HTTP security headers and publicly accessible sensitive directories.
The findings show that the application was not properly hardened and exposed internal information that should never be available to normal users.


Finding 1 – HTTP Security Header Inspection

Severity: Medium
CWE: CWE-693 – Protection Mechanism Failure


Objective:
To inspect the HTTP response headers and verify whether important browser security protections were configured correctly.


Tools Used:
Burp Suite Community Edition
Browser Developer Tools


Steps Performed:
1. Opened OWASP Juice Shop in the browser.
2. Started Burp Suite interception.
3. Browsed to:http://localhost:3000
4. Captured the HTTP response in Burp Suite.
5. Reviewed the response headers for the following security headers:
X-Frame-Options
Content-Security-Policy
Strict-Transport-Security
X-Content-Type-Options
Permissions-Policy


Security Header Results:

| Security Header           | Status  | Observation 
| X-Frame-Options           | Present | SAMEORIGIN configured 
| Content-Security-Policy   | Missing | Increased XSS risk 
| Strict-Transport-Security | Missing | HTTPS not enforced 
| X-Content-Type-Options    | Present | nosniff configured 
| Permissions-Policy        | Missing | Old Feature-Policy used


Result:
Some important security headers were configured correctly, while others were completely missing.
The missing headers weaken browser-side security protections and increase the attack surface of the application.


Security Impact:
Because of the missing headers, attackers may:
1. Attempt cross-site scripting attacks
2. Abuse insecure browser behaviour
3. Perform clickjacking attacks
4. Exploit insecure HTTP communication

Although these issues may not immediately compromise the system, they reduce the overall security strength of the application.


Root Cause:
The application response headers were not fully configured using secure industry standards.
Some modern security protections were either:
1. Missing completely
2. Using outdated configuration
3. Not enforced properly


Recommendation:
The application should:
1. Configure Content-Security-Policy properly
2. Enable Strict-Transport-Security
3. Replace Feature-Policy with Permissions-Policy
4. Perform regular security header reviews


Recommended headers:
Content-Security-Policy: default-src 'self'
Strict-Transport-Security: max-age=31536000
Permissions-Policy: geolocation=()


Evidence to Capture:
Include screenshots showing:
1. Burp Suite response headers
2. URL visible
3. Timestamp visible
4. Missing and present headers clearly visible



Finding 2 – Directory and File Exposure

Severity: High
CWE: CWE-548 – Information Exposure Through Directory Listing


Objective
To verify whether internal directories and sensitive files were publicly accessible without authentication.


Directory Tested – /ftp
URL Accessed:
http://localhost:3000/ftp


Result:
The application exposed an internal directory listing directly through the browser.
Several internal files and backup files were accessible without authentication.


Files Found:
- quarantine/
- acquisitions.md
- announcement_encrypted.md
- coupons_2013.md.bak
- eastere.gg
- encrypt.pyc
- incident-support.kdbx
- legal.md
- package-lock.json.bak
- package.json.bak
- suspicious_errors.yml


Sensitive Files Identified:

| File Name             | Security Risk
| package.json.bak      | Reveals vulnerable dependencies 
| package-lock.json.bak | Reveals exact package versions 
| incident-support.kdbx | May contain credentials 
| encrypt.pyc           | May expose encryption logic 


Security Impact:
Attackers may use these files to:
1. Identify vulnerable software packages
2. Gather internal application information
3. Discover credentials
4. Prepare targeted attacks


Directory Tested – /encryptionkeys:
URL Accessed:
http://localhost:3000/encryptionkeys


Result:
Encryption-related files were publicly accessible without any access restriction.


Files Found:
- jwt.pub
- premium.key


Sensitive Files Identified:

| File Name     | Security Risk 
| premium.key   | May expose cryptographic secrets 
| jwt.pub       | Reveals JWT signing details 


Security Impact:
Exposure of encryption-related files may help attackers:
1. Analyse authentication mechanisms
2. Attempt token-related attacks
3. Compromise encrypted data
4. Bypass security controls


Root Cause:
The application server allowed unrestricted public access to internal directories and sensitive files.
Directory listing was enabled and sensitive files were stored inside publicly accessible locations.


Recommendation:
The application should:
1. Disable directory browsing
2. Restrict access to sensitive folders
3. Remove backup files from production
4. Store encryption keys securely
5. Perform regular deployment reviews


Conclusion:
The application exposed sensitive internal files and lacked proper security hardening.
These weaknesses could help attackers perform deeper exploitation against the system.
