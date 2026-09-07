# Week 7 Lab 01 — Meet the Guard

**Student Name:** David Wright

**Date Completed:** 9/6/2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 7  
**Submission Path:** `week-07/labs/lab-01-meet-the-guard.md`

> ## Cloud Heights Protected-Rules Safety Rule
> Four baseline rules are protected: **100** (`allow-ssh-from-bastion`), **110** (`allow-icmp-intra-vnet`), **120** (`deny-ssh-student-subnet`), and **1000** (`deny-tcp8080-student-subnet` — Inbound Deny TCP from `10.60.6.0/26` to port `8080`). **You never modify, delete, replace, or use a protected rule as a troubleshooting target.** Create or edit student rules only in priorities **200–999**. The priority **1000** fallback deny sits after your band on purpose, so a narrower Allow you create in 200–999 is evaluated first. A mistake in your student range is recoverable and is not a grading penalty when you diagnose it honestly.

> **Evidence safety:** Never include a Cloud Heights password or Bastion shareable URL. Crop browser address bars and login information before committing screenshots.

---

## Mission

Inspect the existing NIC-level security rules on your assigned VM without changing anything. Your goal is to recognize the guardrails, separate protected rules from student-editable space, and map each visible field to the firewall mental model.

## What You Already Know

A network security rule is a decision about traffic. Rules are evaluated from the lowest priority number to the highest, and the first matching rule wins. Inbound and outbound traffic use separate ledgers. A configured service, a security rule, a test result, and an evidence screenshot answer different questions.

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | My Lab Environment → Cloud Heights → Security Rules |
| Change level | Read-only; do not add, edit, or delete rules |
| Expected protected rules | 100 `allow-ssh-from-bastion`; 110 `allow-icmp-intra-vnet`; 120 `deny-ssh-student-subnet`; 1000 `deny-tcp8080-student-subnet` |
| Time | 15–20 minutes |

- [x] I am using my assigned `cf-student-XX` VM through the CyberFoundations Lab Portal.

- [x] The VM shows **Running**.

- [x] I can identify the four protected baseline rules at priorities 100, 110, 120, and 1000.

- [x] I understand that my editable priority range is 200–999.

### Cloud Heights Idle Stop

Cloud Heights may warn you that the VM is idle. Return to the Lab Portal and choose **I'm still working** if you are active. If the VM is stopped or deallocated, it was not deleted: restart it from **My Lab Environment**. Your disk files and saved configuration remain.

## Predict First

Before opening the rule list, predict why a course environment would protect its access and safety rules from student edits.

```text
A course environment would protect its access and safety rules from student edits so students can utilize the environment without being able to modify the controls and protect or govern the environment. This prevents accidental or intentional changes from creating security problems (the more students that can edit a course environment, the more people who can potentially introduce a security risk), inconsistencies (one student can edit a control to the system, and then another student can make a different edit to the system controls that may conflict with the first edit and thus throw the environment into chaos), or disruptions (an edit enacted by one student can potentially cause issues for other students).
```

## Guided Steps

### Step 1 — Open the Guard Post

Start your VM from **My Lab Environment** first. The **Live Azure lab** card is only a launcher — all rule work happens in the Lab Portal's **Security Rules** panel. Do not work in the Azure Portal.

In Cloud Heights, scroll **below** the yellow *Protected rules — do not modify* summary to the detailed list headed **INBOUND — EVALUATION ORDER**. That detailed list, not the yellow summary, is what you inventory and capture.

### Step 2 — Inventory the Baseline

Record each protected rule exactly as shown.

| Priority | Rule name | Direction | Protocol | Source | Destination/port | Action | Protected? |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 100 | allow-ssh-from-bastion | Inbound | TCP | 192.168.10.128/26 | */22 | Allow | Yes |
| 110 | allow-icmp.intra-vnet | Inbound | ICMP | VirtualNetwork | */* | Allow | Yes |
| 120 | deny-ssh-student-subnet | Inbound | TCP | 10.60.6.0/26 | */22 | Allow | Yes |
| 1000 | deny-tcp8080-student-subnet | Inbound | TCP | 10.60.6.0/26 | */8080 | Deny | Yes |

### Step 3 — Map the Fields

For each field, write the question it answers: direction, source, source port, destination, destination port, protocol, action, and priority.

```text
Direction: Is the traffic coming in or out?
Source: Where does the traffic come from?
Source port: Which port is the traffic coming from?
Destination: Where is the traffic going?
Destination port: Which port is the traffic going to?
Protocol:  What kind of traffic is it?
Action: Is the traffic allowed or denied?
Priority: When does the traffic get evaluated?

```

## Stop & Check

- Can you edit a protected rule? You should not be able to — all four are locked.
- Where may student rules be created? Priorities 200–999.
- Which value is read first: 200 or 900? The lower number, 200.

## Test

This is a read-only lab: do not add, edit, or delete any rule. Your test is visual verification — confirm all four protected rules remain present and that no student rule was created.

## Capture Evidence

Capture the detailed **INBOUND — EVALUATION ORDER** view showing all four protected rules (100, 110, 120, 1000) and no student rule. If it does not fit in one image, use two clearly named images and explain why.

## Explain

In 3–4 sentences, explain how protected baselines and a separate student priority band reduce accidental lockout while still allowing meaningful practice.

```text
Protected baselines and a separate student priority band reduce accidental lockout while still allowing meaningful practice by allowing management (but not students) to control protected baseline rules while giving students a designated safe place to experiment with their own rules without overriding or damaging the protected baseline. The student's rules occupy a designated lower-precedence priority band, so they cannot override a protected baseline. Without these guardrails, a student could implement/alter a "deny SSH" rule as a learning experiment and potentially lock other students out of the system. With a protected baseline, students can still experiment with rules such as "deny SSH", but their rules cannot override the protected baseline that preserves critical access.
```

## Required Evidence

Save screenshots in `assets/screenshots/week-07/`:

- `week07-lab01-security-rules-baseline.png`

Open each image at full size before submission. Confirm that no password, Bastion shareable URL, browser address bar, or unrelated private information is visible.

## Analysis Questions

**Analysis Question 1.** Why is a priority number part of rule behavior rather than just an identifier? (Minimum 3 sentences.)

```text
A priority number is part of rule behavior because the priority number determines which rule takes precedence. In Azure Bastion, lower priority numbers are evaluated first-for example, priority 200 is evaluated before priority 250. It is a queue position, not just an identifier-and certainly not a preference or importance rating.
```

**Analysis Question 2.** Explain the difference between a rule being visible, editable, and protected. (Minimum 3 sentences.)

```text
If a rule is visible, it means that you can view it (and its settings). If a rule is editable, it means that you can change/modify it. If a rule is protected, it means that only authorized administrators/managers can modify it.
```

**Analysis Question 3.** Which baseline rule protects your current administrative path, and why must it never be used as a troubleshooting target? (Minimum 3 sentences.)

```text
THe baseline rule that protects a user's current administrative path is priority 100-allow-ssh-from-bastion. It explicitly allows SSH from Azure Bastion, so it is their way into the VM and therefore the backbone of their administrative/management path. Since changing or disabling that baseline could prevent the user from accessing their VM (and thus making their administrative//management work impossible), it should never be used as a troubleshooting target.
```

## Submission Checklist

- [x] Baseline inventory completed without changes

- [x] All visible rule fields mapped to their security questions

- [x] Editable range 200–999 identified

- [x] `week07-lab01-security-rules-baseline.png` captured

- [x] Protected priorities 100, 110, 120, and 1000 were not changed.

- [x] I did not create, edit, or delete any security rules during this read-only lab.

- [x] No password, Bastion URL, or browser address bar appears in my files.

- [x] This worksheet is committed to `week-07/labs/lab-01-meet-the-guard.md`.

## GitHub / Lab Portal Submission

1. Open **Week 7 → Lab 01: Meet the Guard** in the CyberFoundations Lab Portal.
2. Complete every worksheet field and confirm the listed evidence filenames.
3. Upload screenshots to `assets/screenshots/week-07/`.
4. Confirm your portfolio repository is connected, then choose **Submit to GitHub**.
5. Open the committed worksheet and each image on GitHub to verify formatting, legibility, and redaction.

*CyberVisionaries Institute · CyberFoundations · Tier I*
