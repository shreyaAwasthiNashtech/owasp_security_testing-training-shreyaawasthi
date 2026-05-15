Software Supply Chain Failures Findings:

Vulnerability Category:
OWASP Top 10 – A06:2021 Vulnerable and Outdated Components


Introduction:
During testing, the application exposed a backup dependency file named package.json.bak through the publicly accessible /ftp directory.
This file revealed internal third-party dependencies and package versions used by the application. Several outdated and vulnerable packages were identified during dependency analysis.


Objective:
To identify outdated software components and vulnerable third-party libraries used by the application.


Steps Performed   
1. Accessed:
   http://localhost:3000/ftp

2. Downloaded:
   package.json.bak

3. Reviewed dependency versions.

4. Checked vulnerabilities using public vulnerability databases.


Exposed File:
package.json.bak


Vulnerable Packages Identified

| Package         | Installed Version  | Vulnerability            | Severity 
| express-jwt     | 0.1.3              | Authentication bypass    | High 
| sanitize-html   | 1.4.2              | Cross-site scripting     | High 
| js-yaml         | 3.10               | Prototype pollution/DoS  | Medium 
| multer          | ~1.3               | Denial of Service        | Medium


Finding – Vulnerable express-jwt Package

Severity: High
Package Details: express-jwt 0.1.3


Description:
The installed version of `express-jwt` was outdated and contained known authentication validation weaknesses.


Security Impact:
An attacker may:
1. Access protected APIs
2. Bypass login validation
3. Escalate privileges
4. Access restricted data


Root Cause:
The application used outdated third-party dependencies without regular vulnerability monitoring or patching.


Recommendation:
The application should:
1. Upgrade vulnerable packages
2. Enable automated dependency scanning
3. Perform regular dependency reviews
4. Perform regular patch management


Conclusion:
The application used outdated and vulnerable software components which could increase the risk of:
1. Authentication bypass
2. Cross-site scripting
3. Denial of Service
4. Application compromise

Regular dependency management and software supply chain security checks are necessary to reduce these risks.