# Lab 01 — Identity Directory: Who Is Who?

**Learner:** David Wright  
**Attempt:** attempt 075BEA · seed chic-w11-v1 · state revision 1 · text revision 147

> Training simulation — fictional Cloud Heights accounts and resources. Your actions change only your Week 11 learning attempt. This is not a live AD domain, Microsoft Entra tenant or Azure subscription.

## Objective

Investigate why one person may have different access in different identity systems.

## My answers

### Difference 1 between the AD and cloud views (what you saw, and why it matters)

I saw that the AD view list's Alex's AD account (ad-alex) as belonging to the Organizational Unit (OU) OU-RESP, while the cloud view does not list Alex's cloud account (cl-alex) as belonging to any OUs at all. The reason for this is that OUs are strictly an AD concept in this lab exercise. This distinction matters because it shows that you should not automatically assume that an identity is organized, administered, or granted access in the same way across different identity systems just because the accounts represent the same person.

### Difference 2 between the AD and cloud views

I saw that cl-alex is enrolled in MFA, while ad-alex says that MFA is not_in_scope. Therefore, the two accounts have different MFA coverage. This matters because the same person (Alex) has different authentication requirements in different identity systems.

### What do Junior-Analysts and Case-Readers actually grant? How did you check?

The Junior-Analysts group is assigned the RL-LAND (Landing Reader) role, which grants the app_page: read permission on the R-LAND (Analyst Landing) resource. The Case-Readers group is assigned the RL-READ (Case Reader) role, which grants the case: read permission on the R-CASE (Case Summaries) resource. I verified the two groups' access by checking the Groups page to identify each group's assigned role, then checking the Roles and Access page to confirm what permissions each role grants, and finally checking the Resources page to confirm the scope of each assignment (which resource the role applies to).

### Why does Drew's person record still exist?

Drew Patel's person record remains in the directory, even though he has departed the company, so the organization can retain his identity information for administrative and auditing purposes. The retained record also helps the organization manage the offboarding process by tracking Drew's accounts and ensuring that his accounts are disabled and access permissions are revoked to prevent him from accessing company resources.

## Directory trace

| Concept | Object |
|---|---|
| ou | OU-SUP Support |
| role | RL-RESP Response Agent @ R-QUEUE |
| group | GA-RESP Response-Team |
| person | P01 Alex Morgan |
| account | ad-alex (alex@ad.cloudheights.example) |
| identity | ad-alex.department=DEP-RESP |
| permission | queue → update |

## Evidence

- **E01 · EV-075BEA-001** — Directory trace: Alex person, both accounts, OU, one AD grant path, one cloud role path (captured at revision 1)  
  _What this proves:_ These snapshots show one person, Alex Morgan, with two separate accounts-his Active Directory account (ad-alex), and his Cloud Identity account (cl-alex). The evidence shows that MFA is enabled in his Cloud Identity account, while his AD account is marked as out of scope for the MFA requirement. This shows that the two identity systems have different MFA requirements or coverage for Alex's accounts.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-001)
- **E02 · EV-075BEA-002** — Comparison of Blair, Finley and Drew (captured at revision 1)  
  _What this proves:_ These snapshots show one person, Alex Morgan, with two separate accounts: his Active Directory account (ad-alex) and his Cloud Identity account (cl-alex). The evidence shows that MFA is enabled for his Cloud Identity account, while his AD account is marked as out of scope for the MFA requirement. This demonstrates that the two identity systems have different MFA requirements or coverage for Alex's accounts.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-002)
