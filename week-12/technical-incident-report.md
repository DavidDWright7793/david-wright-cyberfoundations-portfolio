# Cloud Heights Identity Investigation — Technical Incident Report

> Fictional training scenario: Cloud Heights Identity Center (simulated). No real organisation, people or systems.

- Analyst: David Wright
- Source case file: [../week-11/labs/lab-06-identity-investigation-case-file.md](../week-11/labs/lab-06-identity-investigation-case-file.md)
- Evidence index: [../week-11/labs/evidence/week11-evidence-index.md](../week-11/labs/evidence/week11-evidence-index.md)

## 1. Purpose / incident context
This report documents the investigation of five failed sign-in attempts followed by a successful authentication involving Casey Rivera's Cloud Identity (cl-casey) account. All six sign-in events occurred within a three-minute period and originated from the same IP address and unregistered device. The five unsuccessful attempts occurred at consistent 30-second intervals, with each failure attributed to an incorrect password. The successful authentication occurred 60 seconds after the fifth failed attempt, although the available records do not specify whether a correct password was entered or another authentication method was used. Although this activity may have a legitimate explanation, the observed pattern warrants further investigation to determine whether it represents unauthorized access or benign user activity.

## 2. Scope
The investigation covered five unsuccessful sign-in attempts followed by one successful authentication involving Casey Rivera's Cloud Identity (cl-casey) account, with all six events originating from the same IP address and unregistered device. All six sign-in events occurred within a three-minute period on September 21, 2026 (14:00:00–14:03:00 UTC). The investigation examined the sequence, timing, authentication outcomes, failure reasons, and source information associated with these events. Particular attention was given to the consistent 30-second intervals between the five unsuccessful attempts, the 60-second interval preceding the successful authentication, and the fact that the first five attempts failed due to incorrect passwords while the authentication method used for the successful attempt was not established. The investigation also considered Casey Rivera's membership in the Response-Operators group (GC-RESP) and the account's identified permissions for the Response Queue and Internal Response Note resources to assess the potential impact of unauthorized access. The investigation was limited to the available sign-in records and identified account permissions; no comprehensive examination of Casey Rivera's Cloud Identity account, the originating device, or account activity following the successful authentication was conducted.

## 3. Evidence reviewed
The following records were reviewed: sign-in logs, captured evidence (EV-075BEA-018, EV-075BEA-019, EV-075BEA-020, EV-075BEA-021).

Evidence IDs (EV-…) and event IDs (S…, A…, C…) refer to records in my Week 11 evidence index; full evidence is not duplicated here.

## 4. Timeline
2026-09-21T14:00:00Z - S004 - Failed authentication attempt involving Casey Rivera's Cloud Identity account from an unregistered device. Failure reason: incorrect password.
2026-09-21T14:00:30Z - S005 - Failed authentication attempt involving Casey Rivera's Cloud Identity account from an unregistered device. Failure reason: incorrect password.
2026-09-21T14:01:00Z	- S006 - Failed authentication attempt involving Casey Rivera's Cloud Identity account from an unregistered device. Failure reason: incorrect password.
2026-09-21T14:01:30Z - S007 -  Failed authentication attempt involving Casey Rivera's Cloud Identity account from an unregistered device. Failure reason: incorrect password.
2026-09-21T14:02:00Z - S008 - Failed authentication attempt involving Casey Rivera's Cloud Identity account from an unregistered device. Failure reason: incorrect password.
2026-09-21T14:03:00Z - S009 - Successful authentication involving Casey Rivera's Cloud Identity account from the same unregistered device.

## 5. Findings
### Finding 1 (RF1) — confidence: likely

The records show that the sign-in activity from Casey Rivera's account is suspicious and warrants further investigation, but the selected evidence does not establish whether the successful sign-in was legitimate or unauthorized.

- Evidence / events: S004, S005, S006, S007, S008, S009
- Uncertainty: The available evidence from the records does not establish who initiated the sign-in attempts, whether the unfamiliar device was authorized, whether MFA was required or bypassed, or whether the successful-sign in resulted in an account compromise.

### Finding 2 (RF2) — confidence: likely

The selected evidence does not contain anything that looks suspicious, and Blair's sign-in attempts should be a low priority for investigation.

- Evidence / events: S002, S003
- Uncertainty: These records do not tell us who signed into Blair's account, or whether they are legitimately authorized to access it.

## 6. Impact / risk
The observed sign-in activity involving Casey Rivera's Cloud Identity account presents a potentially significant security risk to the account and the resources accessible through it. Five unsuccessful sign-in attempts occurred at consistent 30-second intervals, followed by a successful authentication 60 seconds after the fifth unsuccessful attempt. All six events occurred within a three-minute period and originated from the same IP address and unregistered device. The consistent timing of the unsuccessful attempts raises concerns about potentially automated or unauthorized authentication activity, although legitimate user behavior remains a plausible explanation. Additionally, while the first five attempts explicitly identify incorrect passwords as the reason for authentication failure, the successful authentication record does not specify whether a correct password was entered or another authentication method was used.

Casey is a member of the Response-Operators group (GC-RESP) and has read and update permissions for the Response Queue resource, as well as read permission for the Internal Response Note resource. If an unauthorized individual successfully accessed Casey's account, they could potentially view, disclose, or modify Response Queue information and view or disclose Internal Response Notes. Such activity could affect the confidentiality of information contained in these resources and the integrity of Response Queue records. Unauthorized modifications could also disrupt response operations and affect other users who depend on these resources.

Given the account's permissions and the potential consequences of their misuse, the impact of unauthorized access, if it occurred, could be significant. However, the available evidence does not establish that the successful authentication was unauthorized or that any information was accessed, disclosed, or modified. The method used to complete the successful authentication also remains undetermined. Therefore, the actual impact of the incident cannot currently be established.

## 7. Recommendations / next actions
### Recommendation 1 (R1)

- **What:** Within 24 hours, a member of the IT Security team will contact Casey Rivera through the designated communication channel to verify whether Casey initiated the five unsuccessful sign-in attempts and the subsequent successful attempt. If Casey confirms initiating all six attempts, the IT Security team member will ask about the reasons for the five unsuccessful attempts and the authentication method used for the successful sign-in. If Casey does not recognize any of the activity, the IT Security team will promptly escalate the investigation and assess whether additional account protection measures are necessary.
- **Who:** IT Security
- **Why:** This recommended action reduces the risk of unauthorized account access going undetected or unaddressed by verifying whether the sign-in activity was legitimate and identifying whether further investigative or protective measures are necessary.
- **Priority:** medium
- **Timeframe:** within 24 hours
- **Linked findings:** RF1
- **Success measure:** Success will be demonstrated by a documented confirmation from Casey Rivera determining whether they initiated the sign-in attempts, with their explanation checked against the available records. If an issue with the sign-in process is identified and corrected, subsequent sign-in records should show fewer unsuccessful attempts. Any continued unusual sign-in activity would indicate a need for further investigation.

### Recommendation 2 (R2)

- **What:** Within 24 hours, the IT Security team should begin the process of obtaining and reviewing any available additional authentication logs, device registration records, multi-factor authentication policies and any other related records, as well as any account activity following the successful sign-in. The purpose of this review is to determine whether the sign-in activity was authorized, identify how the successful authentication occurred, and establish whether any information was accessed, disclosed, or altered without permission. This review may continue beyond the initial 24-hour period as additional relevant records become available.
- **Who:** IT Security
- **Why:** This recommended action reduces the risk of unauthorized account activity and weaknesses in the sign-in process going undetected or unaddressed, enabling  IT Security and other relevant teams to identify potential security concerns and implement appropriate protective measures.
- **Priority:** medium
- **Timeframe:** within 24 hours
- **Linked findings:** RF1
- **Success measure:** The success of this recommended action will be verified by a documented review of any additional records obtained, including findings about the successful sign-in method, device registration, compliance with authentication policies, and any activity on Casey Rivera's account following the successful sign-in. Any identified security concerns should be documented and addressed, with follow-up checks confirming that appropriate protective measures were implemented.

### Recommendation 3 (R3)

- **What:** There should be continued monitoring of Casey Rivera's Cloud Identity account for unusual sign-in activity, repeated unsuccessful authentication attempts, and unexpected access to or changes in the resources available through the account (as well as any other anomalies). Any concerning or suspicious activity should be investigated promptly, and appropriate protective measures should be taken if unauthorized activity is identified.
- **Who:** IT Security
- **Why:** This recommended action reduces the risk of ongoing or future unauthorized activity going undetected or unaddressed, helping protect Casey Rivera's account and the confidentiality, integrity, and availability of the information and resources accessible through it.
- **Priority:** medium
- **Timeframe:** within 24 hours
- **Linked findings:** RF1
- **Success measure:** The success of this recommended action will be demonstrated by records confirming that monitoring of Casey Rivera's account began within 24 hours and continued throughout the investigation. Monitoring records should show that unusual sign-in attempts, potentially unauthorized access to confidential information, and potentially unauthorized changes to important records were identified, investigated, and addressed when detected.

## 8. Limitations / unknowns
This investigation is limited by the available evidence, which establishes that five unsuccessful sign-in attempts involving Casey Rivera's account were followed by a successful authentication from the same IP address and unregistered device. I do not currently have access to additional authentication logs, device registration records, MFA policies, or account activity following the successful sign-in. Without this additional evidence, it cannot be determined whether the sign-in activity was legitimate or whether Casey's account was compromised.

## 9. Conclusion
Based on the available records, the evidence is insufficient to determine whether the observed sign-in activity involving Casey Rivera's Cloud Identity account was legitimate or unauthorized. Further investigation should include verifying the successful authentication with Casey Rivera and reviewing additional authentication logs, device registration records, MFA policies, and account activity following the successful sign-in. Continued monitoring of Casey's account and its accessible resources is recommended to identify any further unusual authentication activity or unauthorized changes.
