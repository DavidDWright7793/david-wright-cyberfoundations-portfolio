# Week 11 evidence index

Simulator captures from attempt 075BEA. Hash detects content changes; it is not proof of live AD administration.

## EV-075BEA-001

- Slot E01 · M01 · revision 1
- Directory trace: Alex person, both accounts, OU, one AD grant path, one cloud role path
- SHA-256 566bee62701f7da293880123af3cb4ab3f78991b417cde0d9b28e11a22d4934d
- Caption: These snapshots show one person, Alex Morgan, with two separate accounts-his Active Directory account (ad-alex), and his Cloud Identity account (cl-alex). The evidence shows that MFA is enabled in his Cloud Identity account, while his AD account is marked as out of scope for the MFA requirement. This shows that the two identity systems have different MFA requirements or coverage for Alex's accounts.

## EV-075BEA-002

- Slot E02 · M01 · revision 1
- Comparison of Blair, Finley and Drew
- SHA-256 f2f93fb070831494112a8f0e83158ada15eed9c31224c5bf9d4c6e87ae408507
- Caption: These snapshots show one person, Alex Morgan, with two separate accounts: his Active Directory account (ad-alex) and his Cloud Identity account (cl-alex). The evidence shows that MFA is enabled for his Cloud Identity account, while his AD account is marked as out of scope for the MFA requirement. This demonstrates that the two identity systems have different MFA requirements or coverage for Alex's accounts.

## EV-075BEA-003

- Slot E03 · M02 · revision 3
- Successful sign-in + the access result before your change
- SHA-256 a2ec41b7e5c3574b1247776d3791debc73266f67a86233037f1aaa42bdc28751
- Caption: The sign-in record shows that the account authenticated successfully. The access test records that read permission for the Case Summaries resource was denied.

## EV-075BEA-004

- Slot E04 · M02 · revision 8
- Membership/access change audit + read result + update result
- SHA-256 36fcfa3ee0459fabdb07fcffafa13707e2e1c9c467b12243755a158a9662bb02
- Caption: The selected records show that Blair's Cloud Identity account initially denied access to the read permission for the Case Summaries resource. The account was then added to the Case Readers group, which granted it read permission for the Case Summaries resource. An access test was then run on the read permission for Case Summaries, which succeeded. A subsequent access test on the update permission for Case Summaries failed, as only read permission was granted for Case Summaries.

## EV-075BEA-005

- Slot E06 · M03 · revision 15
- Passed verification + reset version change
- SHA-256 bb33863d203eb72477c314baa6d0782ad245c02ab38cafb7844e9b52f3f78a5a
- Caption: The selected records show that a new Active Directory account was created for Jamie Ellis (ad-jamie), the account was added to two Groups (All-Staff and Support-Team), and verification of read permission access for the staff handbook was refused. After that, the records show that the verification of access to that permission was accepted after adding the permission to the account, and a password reset for the account was accepted.

## EV-075BEA-006

- Slot E07 · M03 · revision 32
- Disable / re-enable / session validation sequence
- SHA-256 8b46b04a474ecfc5b116995eaaf2dc02d6fb2df4f7bab2146abd6d0ee7feb683
- Caption: The selected records show Jamie Ellis' Active Directory account (ad-jamie) was disabled and then re-enabled, and then their read permission for the Staff Handbook resource was validated for the account.

## EV-075BEA-007

- Slot E05 · M03 · revision 32
- Created account with OU and groups
- SHA-256 06e67de631bc0d1552184655ef797528c2cca8d3610cdd4be19c0ddf7c5879a6
- Caption: Jamie Ellis' created Active Directory account (ad-jamie) shows that it is in the Support (OU-SUP) Organizational Unit, as well as the All-Staff (GA-ALL) and Support-Team (GA-SUP) Groups.

## EV-075BEA-008

- Slot E08 · M04 · revision 41
- Three job configuration snapshots with rationales
- SHA-256 f6b46c9d7097d31fa1001f4e4069c791b86445909f8786b410bc475cf82cdba0
- Caption: The selected records show that all of the permissions were correct for Blair's and Casey's Cloud Identity accounts. Emi needed to be added to the Audit-Reviewers group, so she was added to it and received its permissions.

## EV-075BEA-009

- Slot E08 · M04 · revision 41
- Three job configuration snapshots with rationales
- SHA-256 dc7c26d408b5add9fe4b789dfa52e13639222f0c6b7050a46922c1e6315230fd
- Caption: The records show that Casey's Cloud Identity account (cl-casey) has delete permissions for the Response Queue resource, which is not allowed  for the account (only read and update permissions are allowed).

## EV-075BEA-010

- Slot E09 · M04 · revision 77
- The nine required access tests
- SHA-256 cd1000c423efd2d5b78652ed3e02ecac79d5ed91d70e334ee3a2a92bbab3ac1d
- Caption: The selected records show testing the permissions of the relevant accounts to ensure the allowed permissions for the account are in place, while the ones that are not allowed are not. They also show that Roles and Access were adjusted for Casey's account in order to give it the least amount of required permissions.

## EV-075BEA-011

- Slot E10 · M04 · revision 81
- Temporary grant → allowed test → revoke → denied retest
- SHA-256 4c865de1fa27f0dc53a45a14c127c01dc580ee9313bcabac014516e20c84bb67
- Caption: The selected records show that Blair's account was granted temporary membership in the Audit-Reviewers group, and a subsequent test allowed the account read permission for the Audit Evidence resource . They then show that  the account's membership in the Audit-Reviewewrs group was revoked, and the subsequent access test for the read permission was denied.

## EV-075BEA-012

- Slot E11 · M04 · revision 90
- Four ABAC cases (current + three what-ifs)
- SHA-256 ea769c8944efcd57419b0f484233bd2b93240e3d774e75eda84e3b9d51d14206
- Caption: The selected records show that all three of the what-if cases resulted in a denial of access.

## EV-075BEA-013

- Slot E12 · M05 · revision 106
- Jamie joiner chain
- SHA-256 c5174008e55c56d62a14350a781fcc0935d688f36a1baf05a12780d4d3838af2
- Caption: The cl-jamie snapshot shows the created account. The account audit snapshots show the account being created, verified, enrolled into MFA, and having its status/credentials changed. They also show Jamie's account being added to two groups. Jamie's joiner access test show that the account is allowed access to read permissons for Case Summaries and denied update permission for  Case Summaries.

## EV-075BEA-014

- Slot E13 · M05 · revision 112
- Alex before/after access and changes
- SHA-256 98565ee69c12bdfae47d332f3a48746e2cdcd282902ba5a0df234f908015976e
- Caption: At this point in Alex's move, the account snapshots and tests show that both accounts (ad-alex and cl-alex) are enabled. They also show that cl-alex has read permission for the Response Queue resource, and that ad-alex has read permission for the Response Share resource.

## EV-075BEA-015

- Slot E13 · M05 · revision 130
- Alex before/after access and changes
- SHA-256 11e563c49868388a0aabe724eb372a73b0c832b0d9eac163be550ba9df2de255
- Caption: At this point in Alex's move, the account snapshots show him being moved from the Response department to the Audit department. They show that the AD account's OU was moved from Response to Audit, and that Alex was removed from the Response group and added to the Audit group in both the AD and CI accounts. The snapshots also show that Alex's Response permissions were removed in both accounts, and Audit permissions were added in both accounts.

## EV-075BEA-016

- Slot E14 · M05 · revision 156
- Finley session/status/revocation evidence
- SHA-256 95ddb5c60107a3a07783f401babe15bb430913293e1ae317f539f97717fc1042
- Caption: The selected records show that Finley's accounts were disabled and their sessions were revoked. They also show that the old-session access retest for his Cloud Identity account failed, and that the new sign-in attemps for both accounts failed.

## EV-075BEA-017

- Slot E15 · M05 · revision 174
- Failed reset verification, refusal and escalation
- SHA-256 1ebb2e999a098689bbe64db33c7c24ed7eef956b7f4e403cd405686743f7f0c2
- Caption: The selected records show the HR ID the caller claiming to be Blair provided (CH-009) does not match with the confirmed HR ID (CH-002). They also show the decision was made not to authorize the password reset and to escalate the request for further verification.

## EV-075BEA-018

- Slot E16 · M05 · revision 180
- AD DS – Entra – Azure comparison and scoped tests
- SHA-256 943c3b9e4dc217f2dd25e28dec78cebefb4f2e387895c5ffe5376d4fd6a5a39a
- Caption: The selected records show that Blair was added to Training-Resource-Readers (GC-AZ) group, which granted him read_metadata permission for the Training-VM resource. They also show the access test for the read_metadata permission succeeded, but the access tests for stop permission failed. The read_metadata permission for Other-Team-VM resource also failed when tested for access.

## EV-075BEA-019

- Slot E17 · M06 · revision 181
- Two distinct findings with raw-event references and correlation
- SHA-256 106ae186693b4ec0efc94d4bf149d475d8609ca7532241da926d20d27708115a
- Caption: Casey Rivera's account made five unsuccessful attempts to sign-in from an unfamiliar device from the same remote location, using the same IP address each time. The sixth authentication attempt was successful, and each of the six attempts occurred within a span of three minutes. One minute after Casey's account successfully authenticated,  it was successfully added to the Privileged-Operators group.

## EV-075BEA-020

- Slot E18 · M06 · revision 181
- Benign/ambiguous comparison
- SHA-256 2f71c05b41daf9291bc2c682b97c992a58e1b4f8985b39d1a8a408f00fb55ba1
- Caption: The selected records show that Casey Rivera's account made six attempts to sign in. The user failed to authenticate five times by entering the password incorrectly, but was successful on the sixth attempt.
