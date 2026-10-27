# Lab 02 — Authentication vs. Authorization: A Valid Badge Doesn't Open Every Door

**Learner:** David Wright  
**Attempt:** attempt 075BEA · seed chic-w11-v1 · state revision 9 · text revision 188

> Training simulation — fictional Cloud Heights accounts and resources. Your actions change only your Week 11 learning attempt. This is not a live AD domain, Microsoft Entra tenant or Azure subscription.

## Objective

Diagnose and repair Blair's missing case access without granting update rights.

## My answers

### Prediction before testing: will Blair be able to read cases? Why?

I predict that Blair will not be able to read cases because Blair's Cloud Identity account (cl-blair) is a member of the Junior Analysts group, which grants read permission to the Analyst Landing resource but does not show a grant of read permission to the Case Summaries resource.

### Identification — using the actual account

Blair's Cloud Identity account (cl-blair) attempted to sign into the system.

### Authentication — using your sign-in event

The account was able to authenticate successfully.

### Authorization — using your access tests

The account was denied access to read permission for Case Summaries, but was allowed access to read permission for Case Summaries after it was added to the Case-Readers group. The account was then denied access to update permission for Case Summaries.

### Accountability — using the audit record

The account was added to the Case-Readers group, which granted it access to read permission for Case Summaries.

## Evidence

- **E03 · EV-075BEA-003** — Successful sign-in + the access result before your change (captured at revision 3)  
  _What this proves:_ The sign-in record shows that the account authenticated successfully. The access test records that read permission for the Case Summaries resource was denied.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-003)
- **E04 · EV-075BEA-004** — Membership/access change audit + read result + update result (captured at revision 8)  
  _What this proves:_ The selected records show that Blair's Cloud Identity account initially denied access to the read permission for the Case Summaries resource. The account was then added to the Case Readers group, which granted it read permission for the Case Summaries resource. An access test was then run on the read permission for Case Summaries, which succeeded. A subsequent access test on the update permission for Case Summaries failed, as only read permission was granted for Case Summaries.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-004)
