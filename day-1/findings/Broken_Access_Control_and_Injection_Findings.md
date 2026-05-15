# Broken Access Control and Injection Findings:

## Vulnerability Category:
OWASP Top 10 – A01:2021 Broken Access Control  
OWASP Top 10 – A03:2021 Injection  

# Summary:
During testing of OWASP Juice Shop, multiple access control weaknesses were identified. The application allowed normal users to perform actions that should only be allowed for authorised users or administrators.
The testing also showed that the application trusted user-controlled input without proper validation, which allowed manipulation of reviews and administrative functionality.

# Finding 1 – Posting a Product Review as Another User

## Severity: High

## CWE: CWE-284 – Improper Access Control

## Objective:
To verify whether a user can modify review details and submit a review using another user’s identity.

## Steps Performed
1. Logged into OWASP Juice Shop using a normal user account.
2. Opened a product page.
3. Added a normal product review.
4. Captured the request using Burp Suite.
5. Sent the request to Burp Repeater.
6. Modified the request body by changing:
   - Review message
   - Author username/email
7. Forwarded the modified request to the server.


## Result:
The application accepted the modified request successfully.
The review appeared in the application as if it had been posted by another user account. This confirmed that the backend trusted user-controlled input instead of validating the authenticated user properly.

## Security Impact:
An attacker may:
1. Impersonate other users
2. Submit fake reviews
3. Damage user reputation
4. Mislead customers
5. Manipulate audit records
In a real-world application, this could reduce trust in the platform and affect business credibility.


## Root Cause:
The application relied on client-side supplied user information instead of validating the logged-in user on the server side.
The backend should always use:
1. Session information
2. JWT token data
3. Server-side authentication context
instead of trusting user input directly.


## Recommendation:
The application should:
1. Ignore user identity fields sent from the client
2. Validate authenticated users server-side
3. Perform ownership checks before processing requests
4. Implement proper access control validation



# Finding 2 – Accessing Administration Section and Deleting 5-Star Reviews

## Severity: Critical

## CWE: CWE-862 – Missing Authorisation


## Steps Performed
1. Observed review data and identified the email:
admin@juice-sh.op
2. Used the discovered administrator account details to access the admin area.
3. Opened browser Developer Tools and inspected network traffic.
4. Located the administration endpoint reference inside:
main.js
5. Navigated to:
/#/administration
6. Accessed the administration functionality successfully.
7. Located review management functionality.
8. Deleted a 5-star review from the administration panel.


## Result:
The application allowed administrative functionality to be accessed and abused.
This confirmed weak access control and insecure exposure of sensitive functionality.

## Security Impact:
An attacker may:
1. Access administrator functionality
2. Delete customer reviews
3. Manipulate application data
4. Abuse privileged functionality
5. Affect business reputation and integrity
In a production system, this could lead to major business and trust impact.


## Root Cause:
Administrative functionality and routes were exposed without sufficient access restrictions.
Sensitive endpoints and privileged operations were discoverable through client-side application files and insufficient access validation.


## Recommendation:
The application should:
1. Enforce strict server-side role validation
2. Restrict access to administrator endpoints
3. Avoid exposing sensitive routes unnecessarily
4. Validate permissions for all privileged actions
5. Perform proper authorisation checks for review deletion


# Conclusion:
The application allowed:
- Review impersonation
- Access to admin functionality
- Deletion of reviews without proper restrictions
This demonstrates insufficient server-side authorisation checks.
