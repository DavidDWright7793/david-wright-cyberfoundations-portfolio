# Week 11 Reflection — IAM & Active Directory

**Student Name:** David Wright

**Date:** 11/2/2026

Answer in your own words. A few sentences each is enough. You do not need to redo your lab answers.

1. What IAM concept became clearer this week?

```text
The concept of AD DS vs. Microsoft Entra ID became clearer to me. They are both directory services that manage identities and help control access to resources, but AD DS generally serves on-premises environments, while Entra ID generally serves cloud environments.
```

2. What is the difference between authentication and authorization, in your own words?

```text
Authentication verifies someone's identity and whether they are allowed into the system, while authorization determines whether they are allowed to access a specific resources within the system.
```

3. Where did least privilege affect one of your decisions?

```text
I removed Casey Rivera's Cloud Identity account from the Privileged-Operators group, as that group's permissions were beyond what Casey required and was approved for.
```

4. What did you learn from a joiner, mover or leaver scenario?

```text
I learned from a leaver scenario that it is important to remove access that is no longer needed for a leaver, as a person leaving an organization who retains unnecessary access to organization information resource can create a significant security vulnerability.
```

5. What made an identity event suspicious versus merely unusual?

```text
One thing that makes an identity event suspicious vs. merely unusual is the presence of multiple irregularities in user activity, as opposed to only one. In my investigation of Casey Rivera's sign-in activity, the account attempted to sign-in unsuccessfully by entering the password incorrectly five times, and then authenticated successfully by entering the correct password on the sixth attempt. All six sign-in attempts came from an unknown device. The presence of both of these factors strengthen the possibility of the activity being suspicious rather than merely unusual, as opposed to if only one of those factors was present.
```

6. What evidence helped support a conclusion you reached?

```text
When I investigated Casey Rivera's sign-in activity, I determined that the presence of several unusual factors (six sign-in attempts with a three-minute timespan, all six attempts coming from an unknown device, lack of clarity on whether MFA was utilized on the successful authentication attempt, etc.) warranted further investigation.
```

7. What uncertainty remained, even after your investigation?

```text
There was enough evidence to determine that Casey Rivera's unusual sign-in activity warranted further investigation, but there was not enough evidence to determine whether the activity was benign (maybe Casey misremembered or mistyped his password five times before getting it right on the sixth attempt) or malicious (an unauthorized individual tried to guess Casey's password and succeeded on the sixth attempt). There was also no way to determine from the available evidence if Casey's account had actually been breached.
```

8. What would you explain differently to a nontechnical manager?

```text
I would explain to a nontechnical manager that authentication is like when you work at a company, your keycard authenticates you and grants you access to the company's building, but once you are inside the building, you need authorization to access certain rooms inside the building. An employee in the Accounting deparment will be authorized to enter the Accounting office (because he needs to go there in order to perform his job duties), but will likely not be authorized to enter the Human Resources office (because he likely does not need to go there in order to perform his job duties).
```

9. What do you want to carry into Week 12, when you turn your case file into an incident report?

```text
I want to hone and develop the skill of translating technical concepts to nontechnical audiences.
```

## Professional Growth Check

- [x] I can explain the difference between authentication and authorization.

- [x] I can describe least privilege with an example from my own work.

- [x] I can walk through a joiner, mover or leaver scenario.

- [x] I can say what made an identity event suspicious, and what evidence supported my conclusion.

- [x] I can name what is still uncertain and what I want to carry into Week 12.
