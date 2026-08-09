# Week 4 Lab — File Permissions: The Badge Audit (CLI Simulator)

**Student Name:** David Wright

**Date Completed:** 8/8/2026

**Module:** 1 — Digital Infrastructure & CLI | **Week:** 4  
**Submission Path:** `week-04/labs/lab-01-file-permissions.md`

---

## Overview

Lesson 1 revealed what Ivy's badge rings mean: every file carries permissions — who may read, write, and execute it — and one wrongly-set ring can be a whole security incident. This lab has you run a small permissions audit of your own in the CLI Simulator: read the rings on a set of seeded files (Part A), fix three problems deliberately with `chmod` (Part B), and read the same story on the Windows side with `Get-Acl` (Part C). One screenshot from this lab becomes part of ★ Deliverable 1.

**Nothing here can break anything real.** The CLI Simulator is a consequence-free practice space — exactly the right place to change permissions for the first time.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | CyberFoundations CLI Simulator (browser-based, inside the Lab Portal) — no install, no VM, no real terminal required |
| Shell | Parts A and B use **bash**; Part C uses **PowerShell** |
| Prerequisite | Week 4, Lesson 1 completed |

**Before you start:** log into the Lab Portal, open **Week 4 → CLI Simulator**, and find the **"Foundry District Badge Office"** scenario. You'll see two entries in the list: **Badge Office — Bash** (used for Parts A and B) and **Badge Office — PowerShell** (used for Part C). Start with the Bash one. It seeds a small folder of files whose permissions have… issues. That's the point.

---

## Part A — Read the Rings

### Step 1 — Get the Security Report

Run the long listing (`ls -l`) in your starting folder. This is the same listing from Week 3's `ls`, with one flag added — and that flag turns it into a per-file security report.

Command you ran:

```
ls -l
```

Output (the full listing):

```
-rw-r--r-- 1 morgan foundry    82 badge-codes.txt
-rw-r--r-- 1 morgan foundry    66 cleanup.sh
-rw-rw-rw- 1 morgan foundry   151 master-inventory.txt
-rw-r--r-- 1 morgan foundry    66 shift-notes.txt
-rw-r--r-- 1 morgan foundry    49 supply-list.txt
```

### Step 2 — Decode One File Completely

Pick any one file from your listing and decode its full permission string, audience by audience — owner, group, other — the way Lesson 1 decoded `-rwxr-xr--`. Write it as plain-English sentences ("the owner can…, the group can…, everyone else can…").

The file and its permission string:

```
-rw-rw-rw- 1 morgan foundry   151 master-inventory.txt

```

Your plain-English decode:

```
The owner can read and and edit (write) the file, but cannot execute it. The group can read and edit the file, but cannot execute it. Everyone else (other) can read and edit the file, but cannot execute it. In other words, all users have the same permissions and restrictions for the file-everybody can read and edit the file, but nobody can execute it.
```

### Step 3 — Find the Problem File

One file in this folder is dramatically more permissive than it should be — every ring lit for every audience, or close to it. Find it. (Hint: scan the *other* triplet — the last three characters — down the whole listing. Which file gives strangers the most?)

The most permissive file and why you flagged it:

```
-rw-rw-rw- 1 morgan foundry   151 master-inventory.txt

This file is the most permissive, as it gives everyone (the owner, group, and users) permission to read AND edit (write) the file. The other files give read and edit permissions to the owner, but only read permissions to everyone else (group and other). Allowing strangers to edit the file is far too permissive.
```

---

## Part B — Change the Rings

This is your first time changing permissions, so we follow THE GATEKEEPER'S RULE on every single change: **check who can touch it now, change it, then check again.** That means `ls -l` before *and after* every `chmod`. The simulator's checklist will verify this — a change without both checks will not pass.

### Step 1 — Lock Down the Problem File

The problem file from Part A, Step 3 should not be writable by the group or by other. Fix it: revoke write from group (`g-w`), then revoke both read and write from other. Run `ls -l` before your first change and after your last one.

Commands you ran (in order, including both ls -l checks):

```
ls -l
chmod g-w master-inventory.txt
chmod o-rw master-inventory.txt
ls -l
```

The file's permission string BEFORE and AFTER:

```
Before: -rw-rw-rw-
After: -rw-r-----
```

### Step 2 — Make a Script Runnable

The scenario seeds a script (its name ends in `.sh`) that its owner cannot currently execute. Grant the owner execute — and only the owner. Verify with `ls -l` after.

Commands you ran:

```
ls -l
chmod u+x cleanup.sh
ls -l

```

Output (the script's corrected permission string):

```
-rwxr--r--
```

### Step 3 — Protect the Secrets File

There's a file whose name makes clear it shouldn't be readable by everyone. Revoke other's read. Verify.

Commands you ran:

```
ls -l
chmod o-r badge-codes.txt
ls -l
```

Output (the corrected permission string):

```
-rw-r-----
```

### Step 4 — Capture Your Audit Evidence (REQUIRED screenshot)

Run one final `ls -l` showing the whole folder with all three fixes in place, and take a screenshot of your simulator session showing it. **This screenshot is required — it is part of ★ Deliverable 1.** Name it `cli-permissions-audit.png`. You'll upload and embed it in the GitHub Commit section below.

---

## Part C — The Same Story, Windows Edition

### Step 1 — Read One File's Guest List

Switch to the PowerShell side of the scenario and run `Get-Acl` on the seeded file the scenario panel points you to. Windows shows a *list* of named accounts and rights instead of three ring-triplets.

Command you ran:

```
Get-Acl shift-notes.txt
```

Output (the owner line and at least one access entry):

```
Path : shift-notes.txt
Owner : morgan
Access : -rw-r--r--
```

### Step 2 — Translate One Entry

Take one access entry from your output and translate it into plain English, the same way you decoded the Linux string in Part A.

Your plain-English translation:

```
Path : shift-notes.txt
Owner : morgan
Access : -rw-r--r--

The file is "shift-notes.txt", and the owner is "morgan". As the owner, "morgan" has permissions to read and edit (write) the file, while the group and everyone else only have permissions to read the file.
```

---

## Analysis Questions

**Analysis Question 1.** In Part A you found the problem file by scanning the *other* triplet. Why is the "other" audience usually the most important one to audit first on a shared system? *(Minimum 2 sentences.)*

```
The "other" audience is the most important audience to audit first on a shared system because they are the audience that (usually) needs the least amount of permissions. There is typically no reason to allow the "other" audience to edit (write) or execute a file, and sometimes it is not even necessary to allow them to read the file. The "other" audience is also the riskiest audience to give excessive permissions to, as they are not vetted in the same way the owner or group are, and nobody knows what they can (or will) do with the file.
```

**Analysis Question 2.** THE GATEKEEPER'S RULE requires a check before *and* after every change, even though `chmod` rarely fails. What does the *before* check protect you from, and what does the *after* check protect you from? *(Minimum 2 sentences.)*

```
In using the "chmod" command, the before check protects you from making a change you do not intend to make by verifying what permissions already exist before you adjust them. The after check protects you by allowing you to make sure that you made the permissions adjustments you intended to, and if you granted or revoked permissions that you did not intend to, you can immediately correct your misstep so it does not cause further problems. That is the Gatekeeper's Rule, in a nutshell.
```

**Analysis Question 3.** Lesson 1 called least privilege "granting what's needed and revoking the rest." Pick one of your three fixes from Part B and explain it in least-privilege terms: what was granted that wasn't needed, and who could have taken advantage? *(Minimum 3 sentences.)*

```
A fix from part B that clearly illustrates "least privilege" is the revocation of edit (write) privileges from the "group" and "other" audiences, and leaving those privileges only with the owner. There is likely no need for the "other" audience to have privileges to edit the file, and granting them those privileges could leave the file vulnerable to being tampered with by a malicious user, since anyone can edit it. It is also probably not necessary for the "group" audience to have privileges to edit the file either, and those privileges should only be granted to them if they are determined to be absolutely necessary for them to perform their job duties.
```

**Analysis Question 4.** Windows ACLs can name specific people; Linux permissions use three fixed audiences. Describe one situation where the Windows approach would be genuinely more useful — and one cost of that extra flexibility. *(Minimum 2 sentences.)*

```
One situation in which the Windows approach would be more useful is if you want to give a group a certain permission on a file, but exclude one specific member of that group. Windows allows you the option of granting a permission to a group, but explicitly denying one specific group member that permission. The downside of this approach is that conflicting allow/deny rules can make troubleshooting more complex and confusing.
```

---

## Submission Checklist

- [x] Full `ls -l` listing recorded (Part A, Step 1)

- [x] One file fully decoded in plain English, all three audiences (Part A, Step 2)

- [x] Problem file identified with evidence from its permission string (Part A, Step 3)

- [x] Problem file locked down with before/after `ls -l` checks recorded (Part B, Step 1)

- [x] Script made owner-executable and verified (Part B, Step 2)

- [x] Secrets file protected from other's read and verified (Part B, Step 3)

- [x] **REQUIRED:** `cli-permissions-audit.png` uploaded to `assets/screenshots/week-04/` and embedded below (Part B, Step 4)

- [x] `Get-Acl` output recorded and one entry translated (Part C)

- [x] All four Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-04/labs/lab-01-file-permissions.md`

---

## GitHub Commit Subsection

This lab's written answers are submitted through the **CyberFoundations Lab Portal**, the same way as Week 3.

1. Go to the CyberFoundations Lab Portal and sign in.
2. Open **Week 4 → Lab 01: File Permissions — The Badge Audit**.
3. Fill in the worksheet fields — they match the commands, outputs, and questions in this file.
4. Connect your GitHub account if you haven't already (one-time setup), and select your portfolio repo.
5. Click **Submit to GitHub**. The Portal commits the completed file to `week-04/labs/lab-01-file-permissions.md` for you.

**📸 REQUIRED — your Deliverable 1 screenshot.** Unlike Week 3's optional screenshot, this one is a graded part of ★ Deliverable 1:

1. Go to your portfolio repository on GitHub.com and navigate to `assets/screenshots/week-04/` (create the folder if this is your first Week 4 screenshot).
2. Click **Add file → Upload files**, drag in your screenshot, named `cli-permissions-audit.png` (lowercase, hyphens, no spaces).
3. Scroll down and click **Commit changes**.
4. Click the uploaded image's filename to open it — the image itself will display on the page.
5. Right-click directly on the image and choose **Copy image address** (Chrome/Edge) or **Copy Image Link** (Firefox).
6. Edit this lab file and paste your copied link into the embed below, at the end of Part B:

![Permissions audit — final ls -l](https://raw.githubusercontent.com/DavidDWright7793/david-wright-cyberfoundations-portfolio/main/assets/screenshots/cli-permissions-audit.png)

**If right-click doesn't show that option** (e.g., on some trackpads or tablets): click the small download-arrow icon in the top-right of the image preview instead, then copy the URL from your browser's address bar.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
