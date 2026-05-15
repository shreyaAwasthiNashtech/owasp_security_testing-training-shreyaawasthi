Documentation Requirement: 

1. Looking at all six vulnerability categories you explored today, which one do you think is most likely to already exist in a project you have worked on, and why? Be honest and specific.

Answer: 
I think the most likely vulnerability that could already exist in a project I worked on is OWASP Security Misconfiguration along with outdated dependencies in a Spring Boot practice project. During development, the focus was mainly on implementing features quickly, so security settings like default configurations, unnecessary error details, weak access settings or unused endpoints may not have been reviewed properly. Also, some libraries and dependencies were added early in the project and were not regularly updated, which could expose the application to known vulnerabilities present in older versions.



2. Five of the six categories (all except A03) have appeared on previous OWASP Top 10 lists. Why do these well-known, well-documented vulnerabilities keep being shipped in production software year after year? Consider the perspective of developers, testers, and management separately.

Answer: 
Even though these vulnerabilities are well known and have been discussed for many years, they still appear in real applications because security is often not given enough importance during development.

From a developer’s point of view, the main focus since years is usually to complete features quickly and finish work well within deadlines. Developers sometimes also believe that the frameworks or libraries they are using already handle security properly, so some security checks and validations get missed.

From a tester’s point of view, most testing is focused on checking whether the application works correctly for users. Security testing is sometimes done very late or not done in enough detail. Testers may also not always have enough security knowledge, time or tools to find complex issues like broken access control or insecure design problems.

From a management point of view, parameters like project deadline, budget and fast delivery are often treated as higher priorities than overall security. Security issues may not seem urgent because users cannot always see them directly. Because of this, known vulnerabilities are sometimes ignored until they cause a serious problem or are found during a security review.



3. A03 (Supply Chain) and A06 (Insecure Design) are both categories where the vulnerability often exists before any functional code is written. What does this tell you about where security testing needs to start in the SDLC?

Answer: 
These categories show that security testing should not begin only after development is complete. Security needs to start at the planning and design stage of the SDLC. Insecure design problems are often created when the application architecture, business logic or validation rules are poorly designed before coding even begins.

Supply chain vulnerabilities also appear early because projects may already depend on outdated or vulnerable third-party packages before developers write their own code. If these risks are not identified early, they become part of the application from the beginning.

This means security should be included in requirement gathering, architecture reviews, dependency management and design discussions. Regular security reviews, dependency scanning and threat modelling should happen throughout the entire SDLC rather than a final testing activity.



4. If you had to pick just three test cases to add to every project's regression suite based on what you discovered today, what would they be and why?

Answer: 
1. Access Control Validation Test
I would always include a test case to check whether a normal user can access admin functions, modify another user’s data or bypass role restrictions. Broken access control vulnerabilities are very common and can lead to serious data exposure or unauthorised actions.

2. Input Validation and Business Logic Test
I would include tests for invalid and unexpected input values such as negative quantities, very large numbers or manipulated request parameters. This is important because many business logic flaws happen when applications trust user input without proper server-side validation.

3. Security Header and Sensitive File Exposure Test
I would add a test case to verify that important HTTP security headers are present and that sensitive directories or backup files are not publicly accessible. Misconfigured servers and exposed files can provide attackers with valuable information about the application and its internal systems.



5. Personal reflection (5–7 sentences): What changed in how you think about testing? Which vulnerability surprised you the most and why?
Answer:
This exercise changed the way I used to think about software testing because I realised that testing is not only about checking whether features work correctly. Security weaknesses can exist even when the application appears to function normally for users. I understood how easily small mistakes in validation, configuration or access control can lead to serious vulnerabilities.

The vulnerability that surprised me the most was the insecure design issue where changing the product quantity to a negative value allowed the total order amount to become negative. I did not expect such a simple input manipulation to completely break the payment logic of the application. It showed me how important server-side validation and business rule checks are.

I was also surprised by how much information could be exposed through publicly accessible directories and backup files. Before this exercise, I mainly focused on expected or functional behaviour but now I understand why security testing must be included from the beginning of development. This assignment helped me think more like an attacker and improved my understanding of how vulnerabilities are discovered in real applications.








