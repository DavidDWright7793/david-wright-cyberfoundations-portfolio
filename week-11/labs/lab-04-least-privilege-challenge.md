# Lab 04 — Least Privilege Challenge

**Learner:** David Wright  
**Attempt:** attempt 075BEA · seed chic-w11-v1 · state revision 95 · text revision 346

> Training simulation — fictional Cloud Heights accounts and resources. Your actions change only your Week 11 learning attempt. This is not a live AD domain, Microsoft Entra tenant or Azure subscription.

## Objective

Configure three job-role assignments, remove excess access, and test role-based and attribute-based access.

## My answers

### Blair, Casey, Emi: job, required actions, forbidden actions

Blair: Junior Analyst, allow read cases permission only, temporary audit-access experiment allowed for training, audit-access not allowed in final state
Casey: Response Agent, approve queue read/update and Internal Response Note read permissions, audit deletion and directory administration are not approved
Emi: Audit Reviewer,  Approve Audit Evidence read and export permissions, deletion is not approved

### Prediction for the three what-if cases, then which attribute changed each result

Device trust override = unmanaged: I predict that access to the permission will be denied.
Department override = Audit (DEP-AUD):  I predict that access to the permission will be denied.
Classification override = Confidential: I predict that access to the permission will be denied.

### RBAC and assignment scope in your own words

RBAC (Role-Based Access Control) is an access control model in which users receive permissions through roles rather than having every permission assigned to them individually. An assignment scope is the resource to which these permissions apply.

### Least privilege — what you removed and why

The concept of least privilege is giving a user only the access needed for the approved task, scope, and duration-in other words, it provides only the access the user actually needs for the job, and nothing more. In this vein, I removed Casey's cloud account from the Privileged-Operators group (GC-PRIV), as that group's permissions were beyond what Casey required and was aproved for.

### Why sign-in didn't settle authorization, and how ABAC adds conditions

Sign-in did not settle authorization because authentication only verifies a user's identity-it does not determine whether the user's account has permission to access a specific resource. ABAC adds conditions to authorization based on attributes of the user or account, the resource, the requested action, and the environment to determine whether access should be allowed.

## Evidence

- **E08 · EV-075BEA-008** — Three job configuration snapshots with rationales (captured at revision 41)  
  _What this proves:_ The selected records show that all of the permissions were correct for Blair's and Casey's Cloud Identity accounts. Emi needed to be added to the Audit-Reviewers group, so she was added to it and received its permissions.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-008)
- **E08 · EV-075BEA-009** — Three job configuration snapshots with rationales (captured at revision 41)  
  _What this proves:_ The records show that Casey's Cloud Identity account (cl-casey) has delete permissions for the Response Queue resource, which is not allowed  for the account (only read and update permissions are allowed).  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-009)
- **E09 · EV-075BEA-010** — The nine required access tests (captured at revision 77)  
  _What this proves:_ The selected records show testing the permissions of the relevant accounts to ensure the allowed permissions for the account are in place, while the ones that are not allowed are not. They also show that Roles and Access were adjusted for Casey's account in order to give it the least amount of required permissions.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-010)
- **E10 · EV-075BEA-011** — Temporary grant → allowed test → revoke → denied retest (captured at revision 81)  
  _What this proves:_ The selected records show that Blair's account was granted temporary membership in the Audit-Reviewers group, and a subsequent test allowed the account read permission for the Audit Evidence resource . They then show that  the account's membership in the Audit-Reviewewrs group was revoked, and the subsequent access test for the read permission was denied.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-011)
- **E11 · EV-075BEA-012** — Four ABAC cases (current + three what-ifs) (captured at revision 90)  
  _What this proves:_ The selected records show that all three of the what-if cases resulted in a denial of access.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-012)
