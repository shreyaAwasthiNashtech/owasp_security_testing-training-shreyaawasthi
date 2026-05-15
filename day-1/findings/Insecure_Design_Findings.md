Insecure Design Findings:

Vulnerability Category
OWASP Top 10 – A04:2021 Insecure Design


Introduction:
During testing of OWASP Juice Shop, multiple business logic weaknesses were identified. The application lacked proper abuse prevention and validation controls.
The vulnerabilities showed that important security checks were missing from the application design itself.



Finding 1 – Automated Feedback Submission

Severity: Medium
CWE: CWE-799 – Improper Control of Interaction Frequency


Objective:
To verify whether customer feedback functionality could be abused using automation.


Tools Used:
Burp Suite Community Edition
Burp Intruder


Steps Performed
1. Logged into OWASP Juice Shop.
2. Submitted a normal feedback request.
3. Captured the request:
POST /api/Feedbacks/
4. Sent the request to Burp Intruder.
5. Added a payload position inside the comment field.
6. Configured number payloads from 1 to 12.
7. Started the Intruder attack.


Result:
Multiple feedback submissions were sent within a short period of time.
The application failed to properly stop automated requests.


Security Impact:
An attacker may:
1. Spam feedback systems
2. Manipulate ratings
3. Flood backend systems
4. Reduce application reliability


Root Cause:
The application lacked:
1. Proper captcha protection
2. Rate limiting
3. Anti-automation controls
4. Abuse prevention mechanisms


Recommendation:
The application should:
1. Invalidate captcha values after use
2. Implement rate limiting
3. Add anti-bot protection
4. Detect automated abuse attempts



Finding 2 – Negative Quantity Manipulation

Severity: High
CWE: CWE-840 – Business Logic Errors


Objective:
To verify whether cart quantity values were validated correctly during checkout.


Steps Performed:
1. Added a product to the basket.
2. Captured the quantity update request.
3. Modified the quantity value to a negative integer.
4. Forwarded the modified request.
5. Proceeded to checkout.


Modified Payload Example

json
{
  "quantity": -100
}


Result:
The application accepted the negative quantity value.
The checkout total became negative, effectively giving money back instead of charging for the purchase.

Security Impact:
An attacker may:
1. Purchase products for free
2. Abuse payment calculations
3. Cause financial loss
4. Manipulate order totals


Root Cause:
The backend failed to validate:
1. Minimum quantity values
2. Numeric boundaries
3. Business logic rules


Recommendation:
The application should:
1. Reject negative quantities
2. Validate quantities server-side
3. Recalculate totals securely
4. Apply strict business logic validation


Conclusion:
The application contained insecure business logic flaws and lacked proper validation controls.
These weaknesses allowed abuse of both feedback functionality and payment calculations.
