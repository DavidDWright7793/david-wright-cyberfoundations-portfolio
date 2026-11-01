# Lab 06 — Identity Investigation + Case File (Deliverable 4)

**Learner:** David Wright  
**Attempt:** attempt 075BEA · seed chic-w11-v1 · state revision 181 · text revision 1094

> Training simulation — fictional Cloud Heights accounts and resources. Your actions change only your Week 11 learning attempt. This is not a live AD domain, Microsoft Entra tenant or Azure subscription.

## Objective

Correlate historical logs and assemble the Cloud Heights IAM Investigation Case File — Portfolio Deliverable 4.

## My answers

### Starting hypothesis before filtering

Casey Rivera's sign-in activity warrants further investigation because it involves five consecutive failed authentication attempts and a successful sign-in within a three-minute period. Each sign-in attempt was from an unfamiliar device and came from the same remote location and IP address. There are several possible explanations for this activity. One relatively benign possibility is that the legitimate account owner mistyped or misremembered the password several times before successfully entering it on the sixth attempt. A more malicious possibility is that an unauthorized individual attempted to gain access to Casey's account by guessing the password and successfully authenticated on the sixth attempt. They could also have known the password but taken six tries to enter it correctly. Another possibility is that the unauthorized individual already knew or had obtained the correct password but made five unsuccessful login attempts before entering it correctly. There is also the matter of the MFA fields-the MFA field contains "not_recorded" for the failed attempts, but "no_challenge_recorded" for the successful attempt. This raises questions about whether an MFA challenge was required, satisfied through another authentication method or session, or just not recorded in the available log data. These factors warrant further investigation of Casey's sign-in activity, but the available evidence is insufficient to determine whether the sign-in activity was legitimate or whether Casey's account was compromised.

## IAM Investigation Case File (Portfolio Deliverable 4)

_This is a technical case file. Week 12 uses it as source material to produce the professional Technical Incident Report and Executive Summary and to finalize and present the portfolio._

### 1. Scope and environment

This investigation examined unusual sign-in activity from Casey Rivera. Casey had five failed sign-in attempts (by entering the password incorrectly) on an unknown device from the same remote location, and successfully authenticated by entering the correct password on the sixth attempt. All of these sign-in attempts occurred within a three-minute span. I examined Casey's records in the historical sign-in log. This examination only posits that Casey's sign-in activity is unusual and warrants further investigation-it does not determine whether the activity is legitimate or malicious, or if Casey's account was breached or not.

### 2. Identity/directory trace and AD DS–Entra–Azure comparison

In this environment, one person is associated with one identity, but that identity can be linked to multiple accounts across directory contexts. For example, Alex Morgan is one person and therefore one identity, but has separate accounts in both Active Directory (ad-alex) and Cloud Identity (cl-alex). Each of Alex's accounts has different group memberships and role assignments, which determine the permissions and resources available to that account.

### 3. Blair authentication-versus-authorization investigation

The sign-in records show that Blair attemped to sign-in to the system but failed to authenticate due to entering the password incorrectly. Blair made another attempt authenticate, and did so successfully by entering the correct password. When Blair signed in successfully, that got them in the door to the system-it did not authorize access to any specific resource.

### 4. Directory administration and sensitive-action verification

During directory administration, I  created an Active Directory account and a Cloud Identity account for Jamie Ellis. I placed the created Active Directory account (ad-jamie) in the Support (OU-SUP) Organizational Unit, as well as the All-Staff (GA-ALL) and Support-Team (GA-SUP) groups. I also placed Jamie's Cloud Identity account (cl-jamie) into two groups, Junior-Analysts (GC-JUN) and Case-Readers (GC-READ) . I also enabled both of Alex's accounts (ad-alex and cl-alex) and performed the relevant tests, which determined that cl-alex has read permission for the Response Queue resource, and that ad-alex has read permission for the Response Share resource.  I also moved Alex from the Response department to the Audit department. I moved Alex's AD account's OU from Response to Audit, and I also removed him from the Response group and added him to the Audit group in both the AD and CI accounts. I also removed Alex's Response permissions from both accounts, and I added Audit permissions in both accounts.

### 5. Three job-role configurations, scopes and business rationales

I determined all of the permissions were correct for Blair's and Casey's Cloud Identity accounts. Emi needed to be added to the Audit-Reviewers group, so I added her to it and she received its permissions. I also determined that Casey's Cloud Identity account (cl-casey) has delete permissions for the Response Queue resource, which is not allowed  for the account (only read and update permissions are allowed). The concept of least privilege is giving a user only the access and permissions necessary to do their jobs-no more, no less.

### 6. Access test matrix and temporary grant/revoke evidence

I tested the permissions of the relevant accounts to ensure the allowed permissions for the accouns are in place, while the ones that are not allowed are not. I adjusted the Roles and Access for Casey's account in order to give it the least amount of required permissions. I granted Blair's account temporary membership in the Audit-Reviewers group, and a subsequent access test I performed determined that account read permission for the Audit Evidence resource was allowed .  Subsequent access tests then showed that the account's membership in the Audit-Reviewers group was revoked, and that the read permission was denied.

### 7. ABAC current-policy and what-if findings

The selected records show that a current-policy access test on Casey Rivera's Cloud Identity account (cl-casey) for read permission on the Internal Response Note resource succeeded , and three subsequent what-if tests failed. The first failed what-if test had the hypothetical condition of a device trust override, the second failed what-if test had the hypothetical condition of a department override, and the third what-if test had the hypothetical condition of a classification override.

### 8. Joiner/mover/leaver and unverified-reset decisions

I created a Cloud Identity account for Jamie Ellis (cl-jamie), and added it to two groups. I gave the account access to read permisson for Case Summaries and denied it update permission for Case Summaries, and confirmed these permissions with a joiner access test. I enabled both of Alex's accounts (ad-alex and cl-alex).I gave cl-alex read permission for the Response Queue resource, and I gave ad-alex read permission for the Response Share resource.  Alex was moved from the Response department to the Audit department. As a result, I moved Alex's AD account's OU from Response to Audit, and also removed Alex from the Response group and added him to the Audit group in both the AD and CI accounts. I also removed Alex's Response permissions in both accounts, and added Audit permissions in both accounts. I disabled Finley's accounts and revoked their sessions. I then performed an old-session access retest for his Cloud Identity account, and it failed. I also performed new sign-in attemps for both accounts, and both attempts failed. I determined that the HR ID the caller claiming to be Blair provided (CH-009) does not match with the confirmed HR ID (CH-002), and made the decision to not authorize the password reset and to escalate the request for further verification.

### 9. Historical identity findings (see findings below)

My historical findings show that Casey Rivera's account made five unsuccessful attempts to sign-in from an unfamiliar device from the same remote location, using the same IP address each time. The sixth authentication attempt was successful, and each of the six attempts occurred within a span of three minutes. One minute after Casey's account successfully authenticated, it was successfully added to the Privileged-Operators group. The selected records show that Casey Rivera's account made six attempts to sign in. The user failed to authenticate five times by entering the password incorrectly, but was successful on the sixth attempt.

#### Finding 1: Casey Rivera's Sign-In Activity

- **Events:** S004, S005, S006, S007, S008, S009
- **Observation:** The selected records show that Casey Rivera's account attempted to sign in five times and failed to authenticate each time, succeeding on the sixth attempt. Each of these sign-in attemps occurred within a three-minute period.  The password was entered incorrectly on the first five attempts, and was successfully entered on the 6th. Each sign-in attempt came from the same remote location and the same IP address. Each attempt was also from an unknown device.
- **Hypothesis:** The sign-in activity for Casey Rivera's account could be legitimate-the user could have mistyped or misremembered the password and entered it incorrectly five times before succeeding on the sixth attempt.
- **Supported conclusion:** The  sign-in activity from Casey Rivera's account is suspicious and warrants further investigation, but the selected evidence does not establish whether the successful sign-in was legitimate or unauthorized.
- **Uncertainty / missing information:** The available evidence from the records does not establish who initiated the sign-in attempts, whether the unfamiliar device was authorized, whether MFA was required or bypassed, or whether the successful-sign in resulted in an account compromise.
- **Next action:** The next action that should be taken in this investigation is to investigate Casey Rivera's sign-in attemps further by reviewing the available authentication logs, device registration records, MFA policies, and account activity following the successful sign-in.
- **Priority:** medium — I classified this investigation as medium priority because five consecutive failed sign-in attempts followed by a successful sign-in from an unfamiliar device raise a legitimate security concern and warrant timely examination. However, there is not yet enough evidence to establish that the activity was unauthorized or that the account was compromised.

#### Finding 2: Blair Chen's Failed Sign-In Attempt

- **Events:** S002, S003
- **Observation:** The selected records show that Blair Chen's account made one unsuccessful sign-in attempt by entering an incorrect passsword, but the account's next authentication attemp was successful and the password was correctly entered.
- **Hypothesis:** It is possible that Blair simply mistyped the account's password the first time and then typed it correctly the second time, resulting in successful authentication.
- **Supported conclusion:** The selected evidence does not contain anything that looks suspicious, and Blair's sign-in attempts should be a low priority for investigation.
- **Uncertainty / missing information:** These records do not tell us who signed into Blair's account, or whether they are legitimately authorized to access it.
- **Next action:** This finding does not seem overly suspicious, so nothing needs to be done except to continue monitoring Blair's sign-in attempts in case any suspicious activity does occur.
- **Priority:** low — This investigation should be low priority because the probability of one failed sign-in attempt before succcessful authentication is unlikely to indicate unauthorized activity.

### 10. Sign-in/audit correlation and one benign/ambiguous comparison

In the sign-in logs, Casey Rivera's account made six attempts to sign in. The user failed to authenticate five times by entering the password incorrectly, but was successful on the sixth attempt. In the audit logs, Casey's Cloud Identity account (cl-casey) was moved to the Privileged-Operators group. A benign explanation of these events and the link between them could be that Casey mistyped or misremembered his password five times but successfully authenticated on his sixth attempt, and then moved his Cloud Identity account to the Privileged-Operators group. It is still ambiguous whether that is the case or an unauthorized user incorrectly guessed the account password five times and was successful on the sicth attempt, or if Casey's account was breached or not-there is not enough evidence at this point in time to make a determination either way.

**Benign/ambiguous comparison** (S004, S005, S006, S007, S008, S009, S002, S003): These records show failed sign-in attempts before successful authentication from two accounts. One of these accounts had five failed sign-in attenpts before successful authentication on the sixth attempt, and each of the attemots occurred within a three-minute span. Each sign-in attempt also comes in from an unknown device. This looks potentially suspicious, like an unauthorized individual could have tried guessing the password five times before getting it right on the sixth attempt. On the other hand, the user could be legitimate and have just mistyped or misremembers their password before typing the correct password on the sixth try.

**Live simulator chain (current attempt, not historical):** AT-075BEA-109-1 AT-075BEA-112-1 AT-075BEA-123-1 AT-075BEA-124-1 AT-075BEA-125-1 AT-075BEA-129-1 AT-075BEA-130-1

The above access-test records show that both accounts (ad-alex and cl-alex) are enabled. They also show that cl-alex has read permission for the Response Queue resource, and that ad-alex has read permission for the Response Share resource.  The access-test records also show that Alex's Response permissions were removed in both accounts, and Audit permissions were added in both accounts.

### 11. Preliminary response/remediation recommendations, priority and uncertainty

The next action I recommend is to investigate Casey Rivera's sign-in attempts further by reviewing the available authentication logs, device registration records, MFA policies, and account activity following the successful sign-in. This will help determine whether the activity was consistent with Casey's normal sign-in behavior or may have involved unauthorized access. Casey should also be asked to confirm whether they recognize the device and initiated the sign-in attempts. I recommend assigning this inevstigation a priority of medium, because the activity is suspicious/unusual enough to warrant timely investigation, but the evidence does not yet establish an active compromise.

### 12. Evidence index notes

My Case File relies on the event IDs S004, S005, S006, S007, S008, and S009 in the sign-in logs, and A002 in the audit logs.

### Explicit simulation/environment limitations

This investigation is limited by the fact that I only know that Casey attempted to sign-in unsuccessfully five times from an unknown device before authenticating successfully on the sixth attempt. I do not currently have access to further authentication logs, device registration records, MFA policies, or account activity following the successful sign-in. Without this further evidence, it cannot be determined whether the sign-in activity was legitimate, or if Casey's account was actually breached.

### Earlier labs

- [Lab 01](lab-01-identity-directory.md)
- [Lab 02](lab-02-authentication-vs-authorization.md)
- [Lab 03](lab-03-build-and-manage-directory.md)
- [Lab 04](lab-04-least-privilege-challenge.md)
- [Lab 05](lab-05-joiner-mover-leaver.md)

## Evidence

- **E17 · EV-075BEA-019** — Two distinct findings with raw-event references and correlation (captured at revision 181)  
  _What this proves:_ Casey Rivera's account made five unsuccessful attempts to sign-in from an unfamiliar device from the same remote location, using the same IP address each time. The sixth authentication attempt was successful, and each of the six attempts occurred within a span of three minutes. One minute after Casey's account successfully authenticated,  it was successfully added to the Privileged-Operators group.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-019)
- **E18 · EV-075BEA-020** — Benign/ambiguous comparison (captured at revision 181)  
  _What this proves:_ The selected records show that Casey Rivera's account made six attempts to sign in. The user failed to authenticate five times by entering the password incorrectly, but was successful on the sixth attempt.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-020)
- **E19 · EV-075BEA-021** — Completed case file / versioned export (captured at revision 181)  
  _What this proves:_ The selected records show Casey Rivera unsuccessfully attempting to sign-in five times by entering the password incorrectly, and successfully authenticating on the sixth attempt by entering the correct password. Each of the six sign-in attempts came from the same IP address, same remote location, and from an unknown device. All six sign-in attempts occurred within a three-minute timespan.  
  See [evidence index](evidence/week11-evidence-index.md#ev-075bea-021)
