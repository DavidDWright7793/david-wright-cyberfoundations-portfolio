# Lab 05 — Joiner, Mover, Leaver

**Learner:** David Wright  
**Attempt:** attempt 075BEA · seed chic-w11-v1 · state revision 181 · text revision 425

> Training simulation — fictional Cloud Heights accounts and resources. Your actions change only your Week 11 learning attempt. This is not a live AD domain, Microsoft Entra tenant or Azure subscription.

## Objective

Complete four lifecycle tickets across the two directory surfaces, plus a short Azure scope comparison.

## My answers

### T501 decision table — Add / Retain / Remove / Deny / Escalate (write 'not applicable — reason' where needed)

Add-: Junior-Analysts, Case-Readers
Retain: not applicable
Remove: not applicable
Deny: update permission for Case-Summaries
Escalate: not applicable

### T502 decision table — Add / Retain / Remove / Deny / Escalate

Add: GC-AUD, GA-AUD,  OU-AUD
Retain: GA-ALL
Remove:  GA-RESP, GC-AUD
Deny: not applicable
Escalate: not applicable

### T503 decision table — Add / Retain / Remove / Deny / Escalate

Add: OU-DIS
Retain: records and audits
Remove: all group memberships
Deny: not applicable
Escalate: not applicable

### T504 decision table — Add / Retain / Remove / Deny / Escalate

Add: not applicable
Retain: not applicable
Remove: not applicable
Deny: password reset
Escalate: password reset request

### Why is an Azure resource role/scope different from a cloud directory role?

An Azure resource role/scope differs from a cloud directory role in that Azure resource roles control what actions a user can perform on Azure resources, while the scope determines which resources these permissions apply to. In contrast, cloud directory roles control what administrative actions a user can perform within the identity directory.

## Evidence

- **E12 · EV-075BEA-013** — Jamie joiner chain (captured at revision 106)  
  _What this proves:_ The cl-jamie snapshot shows the created account. The account audit snapshots show the account being created, verified, enrolled into MFA, and having its status/credentials changed. They also show Jamie's account being added to two groups. Jamie's joiner access test show that the account is allowed access to read permissons for Case Summaries and denied update permission for  Case Summaries.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-013)
- **E13 · EV-075BEA-014** — Alex before/after access and changes (captured at revision 112)  
  _What this proves:_ At this point in Alex's move, the account snapshots and tests show that both accounts (ad-alex and cl-alex are enabled. They also show that cl-alex has read permission for the Response Queue resource, and that ad-alex has read permission for the Response Share resource.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-014)
- **E13 · EV-075BEA-015** — Alex before/after access and changes (captured at revision 130)  
  _What this proves:_ At this point in Alex's move, the account snapshots show him being moved from the Response department to the Audit department. They show that the AD account's OU was moved from Response to Audit, and that Alex was removed from the Response group and added to the Audit group in both the AD and CI accounts. The snapshots also show that Alex's Response permissions were removed in both accounts, and Audit permissions were added in both accounts.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-015)
- **E14 · EV-075BEA-016** — Finley session/status/revocation evidence (captured at revision 156)  
  _What this proves:_ The selected records show that Finley's accounts were disabled and their sessions were revoked. They also show that the old-session access retest for his Cloud Identity account failed, and that the new sign-in attemps for both accounts failed.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-016)
- **E15 · EV-075BEA-017** — Failed reset verification, refusal and escalation (captured at revision 174)  
  _What this proves:_ The selected records show the HR ID the caller claiming to be Blair provided (CH-009) does not match with the confirmed HR ID (CH-002). They also show the decision was made not to authorize the password reset and to escalate the request for further verification.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-017)
- **E16 · EV-075BEA-018** — AD DS – Entra – Azure comparison and scoped tests (captured at revision 180)  
  _What this proves:_ The selected records show that Blair was added to Training-Resource-Readers (GC-AZ) group, which granted him read_metadata permission for the Training-VM resource. They also show the access test for the read_metadata permission succeeded, but the access tests for stop permission failed. The read_metadata permission for Other-Team-VM resource also failed when tested for access.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-018)
