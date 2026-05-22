# Day 2 - Core Concepts & Assessment Findings

## Core Concept Questions & Answers


## Question 1: Testing Approach - Juice Shop vs DVWA

**How did your testing approach change between Juice Shop and DVWA? What did you prioritize, and what did you almost miss?**

### Answer:

The first thing I prioritised was mapping the application manually. I clicked every menu, submitted normal values before malicious ones, and tried to understand how the application behaved normally before attempting exploitation. Before starting the testing properly, I revised the vulnerability concepts again using Google and my session notes because this time there were no hints available. I focused on understanding what kind of behaviour usually indicates a vulnerability. 

For example, whenever I noticed user input getting reflected in the URL or directly displayed back on the page, I immediately started testing common injection payloads manually. Similarly, if I saw parameters changing in the URL during sensitive actions like password changes, I explored whether those requests could be manipulated directly. 

I also started paying much more attention to small behavioural clues instead of only looking for successful payloads. Sometimes even an error message, unusual redirect, or reflected HTML gave hints that something insecure was happening underneath.

Unlike Juice Shop where the goal was mostly to solve the challenge, DVWA felt more like real investigation work where I had to observe patterns, think logically, search for ideas, and test different possibilities patiently until something meaningful appeared.


## Question 2: Manual Testing vs Automated Scanners

**What did manual testing allow you to find or understand that an automated tool would have missed? Give at least two specific examples.**

### Answer:

Automated tools can definitely work faster and are very useful for identifying many common vulnerabilities quickly. However, during this assessment I realised that manual testing develops a completely different skillset. It forces us to think logically and critically instead of depending entirely on tools to tell us what is vulnerable.

While testing manually, I had to observe application behaviour carefully, understand how requests and responses were working, and think about why something looked insecure rather than simply trusting a scan result. This helped me understand the actual root cause behind the vulnerabilities instead of only recognising their names.

I also feel manual testing is important because tools and services may not always be available. There can be situations where scanners fail, services are down, payloads are blocked, or the vulnerability does not match a known pattern. In those cases, a tester's own understanding and thought process become more valuable than automation itself. A person who can think independently still has the ability to identify weaknesses and help protect the system even without specialised tools.

Another important thing I noticed is that automated tools mainly focus on known or predefined vulnerability patterns. Manual testing, on the other hand, allows a tester to explore application logic, unusual behaviour, weak workflows, and small inconsistencies that may not exist in vulnerability databases or standard signatures. Sometimes a small observation during manual testing can lead to a much bigger finding that an automated scanner may completely overlook or misinterpret.


## Question 3: Most Critical Finding - Command Injection

**Choose the single most critical finding from your assessment. Explain it to a CEO with no technical background.**

### Answer:

The most critical issue is **Command Injection**, because it goes beyond just data exposure and can affect the actual system running the application.

In simple terms, it's like using a normal website feature and that request secretly ends up controlling the underlying computer itself. It's similar to telling a shop assistant to "check stock", but the instruction is manipulated so the shop's entire computer starts running unintended actions like opening files or changing system settings.

**Everyday example:** It's like ordering food delivery and instead of just placing your order, the request makes the restaurant's computer open internal records or execute hidden system tasks you never asked for.

**Why it matters to the business:** This is extremely serious because it can potentially give an attacker control over the server itself, not just the data. This makes it one of the most dangerous vulnerabilities in any web application where anyone could steal everything, delete everything, or shut the whole system down.


## Question 4: Defence in Depth - Security Levels

**What do you think Medium security does differently for the two most critical vulnerabilities? What does this tell you about defence in depth?**

### Answer:

#### SQL Injection Vulnerability:

For the SQL Injection vulnerability, I believe the Medium security level probably introduces stronger input handling and validation. Instead of accepting raw user input directly into database queries, it may sanitise characters, restrict unexpected input formats, or use safer query methods. That would make basic payloads fail even if the underlying feature still exists.

**Defence in Depth:** However, if this layer is bypassed, other protections such as parameterised queries, database permission restrictions, and query structure controls should still prevent full data exposure. If one security layer fails, the others remain standing.

#### Command Injection Vulnerability:

For the Command Injection vulnerability, Medium security likely adds additional filtering on user inputs, blocking special characters or command separators that are commonly used to chain system commands. It may also restrict how system-level functions are called from the application. 

**Defence in Depth:** Even if an attacker manages to bypass input filtering, proper defence-in-depth should ensure that:
- The application runs with limited system privileges
- Command execution is isolated from critical system resources
- Strict allow-lists are enforced so only intended operations are possible

#### Overall Lesson:

This shows the importance of defence in depth: **if one security layer fails, other layers should still stand strong and reduce the impact of the attack rather than allowing complete compromise.** No single security control is perfect—layered protections ensure that even if one is broken, the system remains protected.


Link for the Report- https://wearenashtech-my.sharepoint.com/:w:/r/personal/shreya_awasthi_nashtechglobal_com/Documents/DVWA%20Assignment%20Report.docx?d=w231605326f274021b359a75553c75a32&csf=1&web=1&e=X13l5U