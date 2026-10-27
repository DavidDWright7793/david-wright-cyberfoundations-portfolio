# Lab 03 — Build and Manage the Directory

**Learner:** David Wright  
**Attempt:** attempt 075BEA · seed chic-w11-v1 · state revision 36 · text revision 258

> Training simulation — fictional Cloud Heights accounts and resources. Your actions change only your Week 11 learning attempt. This is not a live AD domain, Microsoft Entra tenant or Azure subscription.

## Objective

Create Jamie's AD account, place it, grant basic group access, and verify, reset and enable it safely.

## My answers

### What did OU placement change — and not change?

In Jamie Ellis' AD account (ad-jamie), placing the account into the Support OU (OU-SUP) changed how the account is organized and whch administrative policies may apply to it. This placement influenced which Group Policy settings apply to the account and which administrators are authorized to manage the account. Placing the account into the Support OU did not automatically change its security group memberships or resource permissions.

### What did group membership change?

When Jamie's AD account (ad-jamie) was placed into the All-Staff  (GA-ALL) and Support Team (GA-SUP) Groups, it changed what resources and permissions the account could access. Placement into those groups did not change the account's OU (OU-SUP), account identity, or password.

### What did the credential reset change? Why did verification come first?

The credential reset for the account changed the account's sign-in credentials, and verification came first to ensure that the person requesting the reset was authorized to do so.

### What did disabling and re-enabling do to sessions and access?

When Jamie's AD account was disabled and re-enabled, its ability to authenticate was changed. However, its access permissions were left unchanged.

## Evidence

- **E06 · EV-075BEA-005** — Passed verification + reset version change (captured at revision 15)  
  _What this proves:_ The selected records show that a new Active Directory account was created for Jamie Ellis (ad-jamie), the account was added to two Groups (All-Staff and Support-Team), and verification of read permission access for the staff handbook was refused. After that, the records show that the verification of access to that permission was accepted after adding the permission to the account, and a password reset for the account was accepted.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-005)
- **E07 · EV-075BEA-006** — Disable / re-enable / session validation sequence (captured at revision 32)  
  _What this proves:_ The selected records show Jamie Ellis' Active Directory account (ad-jamie) was disabled and then re-enabled, and then ther read permission for the Staff Handbook resource was validated for the account.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-006)
- **E05 · EV-075BEA-007** — Created account with OU and groups (captured at revision 32)  
  _What this proves:_ Jamie Ellis' created Active Directory account (ad-jamie) shows that it is in the Support (OU-SUP) Organizational Unit, as well as the All-Staff (GA-ALL) and Support-Team (GA-SUP) Groups.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-007)
