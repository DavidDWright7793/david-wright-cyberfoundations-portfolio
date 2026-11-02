# Week 11 Notes — IAM & Active Directory

**Student Name:** David Wright

**Date:** 11/2/2026

Use your own words and everyday examples. These notes support your thinking; they are not your lab answers. Do not copy your lab answers here — those belong in the Cloud Heights Identity Center.

## 1. Person vs Identity vs Account

```text
A person is: A person is an individual human being.
An identity is: An identity is the digital represenation of that person within a system.
An account is: An account is a record associated with that identity that allows the peson to access resources and services-one person can have multiple accounts across different systems or directories.
An everyday example that shows the difference: An everyday example that shows the difference between these concepts is that I am one person (David Wright) with one identity represented across different organizations. I have one account at my local bank and another account at my local gym. Both accounts are associated with me (David Wright), but they are separate records maintained by two different organizations.
```

## 2. OU vs Group vs Role vs Permission

```text
An organizational unit (OU) is: A container that organizes directory objects.
A group is: A collection of users or accounts that can be assigned roles or permissions.
A role is: A bundle of permissions than can be assigned to a principal.
A permission is: An allowed action on a resource.
How they fit together in one sentence: An OU organizes directory objects, such as users and groups; groups collect users or accounts; roles define what actions those users or accounts can perform; and permissions specify the particular actions allowed on a resource.
```

## 3. Authentication vs Authorization

```text
Authentication means: Authentication means verifying that someone is who they claim to be.
Authorization means: Authorization means determining whether someone has permission to access a specific resource or perform a particular action.
A real-life analogy (for example, an airport or an office building): Mike Smith works in the Accounting department at Mega Corporation. His keycard grants him access to the company's building, as his identity has been verified and he has been granted permission to enter the building. However, Mike is not authorized to enter the Human Resources office because his job responsibilities do not require access to that area. Therefore, even though Mike has successfully authenticated with his keycard and gained access to the Mega Corporation building, his keycard will not grant him access to the HR office (an area he is not authorized to enter).
```

## 4. Least Privilege

```text
Least privilege means: The principle of least privilege means giving a user only the access or permissions necessary to perform their job duties-no more and no less.
One place in the labs where giving more access would have been risky: When Emi was given read and export permission for Audit Evidence, she was not given delete permission. Giving her delete permission if she did not truly need to to perform her job duties would have been risky, as deletion is sensitive and often hard to undo.
```

## 5. RBAC

```text
Role-based access control means: Access that is assigned based on roles.
One role from the labs and what it allowed: RL-RESP Response Agent - queue: read, update; response_note: read
```

## 6. ABAC

```text
Attribute-based access control means: Access that is assigned based on attributes, such as department, resource classification, or managed-device status.
How it differs from RBAC: In RBAC, access policy follows job roles; in ABAC, access policy follows contextual properties.
```

## 7. AD DS vs Entra ID

```text
AD DS is: A directory service that organizes and manages domains (and their objects) for on-premises network resources.
Microsoft Entra ID is: Microsoft's cloud identity and access management service.
One similarity and one difference: Both AD DS and Microsoft Entra ID are directory services that manage identities and support authentication and access management for users, groups, and other resource. Their main difference is that AD DS generally serves on-premises environments, while Entra ID generally serves cloud environments.
```

## 8. Azure Resource RBAC

```text
What Azure resource RBAC controls: Azure resource RBAC controls access to Azure resources by assigning roles to users, groups, or service identities at a specific scope.
How it relates to what I did in the simulator: In the simulator, I added Blair Chen's Cloud Identity account to the Case Readers group, which granted it read permission for the Case Summaries resource.
```

## 9. Joiner / Mover / Leaver

```text
Joiner (what happens when someone starts): A joiner is a person beginning a role in the organization who needs verified, approved access. For a joiner, you verify the approved role and start time, and then provision a named account and necessary access.
Mover (what happens when someone changes roles): A mover is a person changing roles within the organization whose old and new access needs review. For a mover, you review new duties, grant necessary new access and remove unnecessary old access with appropriate timing.
Leaver (what happens when someone leaves): A leaver is a person leaving the organization whose access must be ended under the process. For a leaver, you disable access, end sessions where policy requires and manage work ownership at the authorized end time.
Why the leaver step matters most for security: The leaver step matters most for security because when someone leaves an organization, there access to organizational resources must be revoked. If their accounts remain active, they may retain access to information and systems they are no longer authorized to use, creating a significant security vulnerability.
```

## 10. Sign-in Logs vs Audit Logs

```text
Sign-in logs show: Sign-in logs show a record of authentication activity, including the attempt and result.
Audit logs show: Audit logs show a record of an operation or change, often with actor and target.
One question each log can answer: Sign-in log: What was attempted and what happened?
Audit log: Which operation changed what?
```

## 11. Useful Terms and Questions

```text
Terms I want to review: RBAC, ABAC, Azure Resource RBAC
Questions for my instructor: n/a
```
