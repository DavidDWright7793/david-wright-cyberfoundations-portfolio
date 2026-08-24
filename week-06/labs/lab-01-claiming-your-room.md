# Week 6 Lab 01 — Claiming Your Room in Cloud Heights

**Student Name:** David Wright

**Date Completed:** 8/24/2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 6  
**Submission Path:** `week-06/labs/lab-01-claiming-your-room.md`

---

> ### 🔒 Cloud Heights Security Rule
> Your Bastion link and Cloud Heights password are **private access credentials**. Never paste either into a worksheet, screenshot, GitHub repository, Circle post, or chat message. When taking screenshots, crop out the browser address bar and all login information.

---

## Overview

Week 5 was practice. This week the machine is real. Cloud Heights is a live Ubuntu 22.04 server running in Azure, and one of its rooms has **already been reserved for you** — you do not create it, provision it, or pay for it. Your job in this lab is to walk in the front door, prove you are standing inside your own room, and understand where that room came from.

This is a **guided** lab. Every step tells you what to do and what to record. Expect 30–40 minutes.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | Cloud Heights — live Ubuntu 22.04 VM in Azure, reached through Azure Bastion in your browser |
| Access | Lab Portal → **My Lab Environment** → your Cloud Heights card |
| Username | `analyst` |
| Password | Provided to you separately. Never typed into this worksheet. |
| Commands used | `hostname`, `whoami`, `pwd` |
| Auto-shutdown | Your VM stops automatically after 15 minutes of inactivity. A warning with **Keep Working** appears first. |

**Before you start:** open **My Lab Environment** in the Portal. If your VM shows **Stopped**, click **Start VM** and wait until the status reads **Running** — this takes a minute or two. Only then click **Open Cloud Heights**.

---

## Part A — Walking In

### Step 1 — Start the Room

In **My Lab Environment**, check your Cloud Heights status. Start the VM if it is stopped and wait for **Running**.

The status you saw before you started, and the status you saw after:

```
The status I saw before I started the VM was "Stopped", and the status I saw after I started the VM was "Running".
```

### Step 2 — Open Cloud Heights and Sign In

Click **Open Cloud Heights**. A browser-based session opens through Azure Bastion. Sign in with username `analyst` and the password you were given separately.

**Do not record the password, the link, or any part of the login screen anywhere.**

Describe what you saw once the session opened — what kind of screen greeted you:

```
Once the session opened, I was greeted by a screen that looked like a Linux terminal. It was obviously an Ubuntu terminal, but it was made clear that the terminal was a training environment for CyberVisionaries.
```

### Step 3 — Ask the Machine Its Name

Run:
```
hostname
```
Output:

```
cf-student-04
```

### Step 4 — Ask Who You Are

Run:
```
whoami
```
Output:

```
analyst
```

### Step 5 — Ask Where You Are Standing

Run:
```
pwd
```
Output:

```
/home/analyst
```

---

## Part B — What Those Three Answers Prove

### Step 1 — Read Them as Evidence

Each of those three commands answered a different question: *which machine*, *which identity*, *which location in the filesystem*. Together they are the proof that you are inside your own room and not somebody else's.

Explain, in your own words, what each output proves:

```
The hostname command answers the question of "which machine am I on?". The whoami command answers the question of "which account am I using?". The pwd command answers the question of "where am I in the file system?".
```

### Step 2 — Capture Your Evidence

Take a screenshot of your terminal showing the three commands and their outputs.

**Required filename:** `bastion-session.png`

**Crop rules — not optional.** The screenshot must show the terminal and prompt. It must **not** show the browser address bar, the Bastion link, any login screen, or any password field. Crop before you upload.

Upload it to `assets/screenshots/week-06/` in your portfolio repository, then paste its link here:

---

## Part C — Where Your Room Came From

### Step 1 — The Golden Image Idea

Every student's Cloud Heights room was built from the **same standardized image** — a known-good snapshot of a configured Ubuntu machine. Nobody hand-built 20 servers. One machine was configured correctly once, captured, and stamped out repeatedly.

Explain in your own words what a standardized (golden) image is and why an organization would build one:

```
A standardized (golden) image is one carefully built, known-good, and verified machine that every new machine is stamped from, so no one starts with a broken build. If everyone starts with the same known-good machine, we know that everyone has a machine that works properly. Also, if everyone starts with the same machine and there is a problem, that problem would likely apply to everybody and thus be easier to solve. It is much easier to solve one problem that 20 people have than to solve 20 different problems that one person each has.
```

### Step 2 — Same Start, Different Rooms

Your room started identical to everyone else's, and from today it starts to diverge as you work in it.

Explain what stays the same across all the rooms and what becomes yours alone:

```
In each room, the underlying infrastructure remains under the provider's control and thus stays the same across all rooms. This includes the physical building, physical hardware (servers, storage, networking, power/cooling), and the cloud platform infrastructure. What changes in each individual room as students work in them is the VM/guest environment. Elements of this that are customizable by individual students include user accounts, passwords/credentials, permissions, data, applications, configurations, and access decisions.
```

---

## Analysis Questions

**Analysis Question 1.** Why does it matter that a standardized image can be *restored*, not just deployed? Describe a realistic situation where restoring from a known-good image is the fastest safe fix. *(Minimum 3 sentences.)*

```
The fact that a standardized (golden) image can be restored, not just deployed, is a signficant testament to its usefulness. Restoring from a known-good image is the fastest safe fix in situations where you need to recover quickly (possibly to meet a strict deadline) and the cause of the problem isn't worth spending time diagnosing before recovery. One example of such a scenario is when a VM becomes unstable shortly before a critical deadline. If the deadline is fast approaching, restoring from a known-good image is a more prudent solution than spending hours troubleshooting the accumulated changes, as the priority would need to be getting the system back into service quickly.
```

**Analysis Question 2.** Conceptually, how is a snapshot different from a separate backup? Consider what each one protects against and where each one lives. *(Minimum 3 sentences.)*

```
A snapshot is a point-in-time copy or state of a system or disk, taken before a significant change, that enables the user to quickly return to that state. A backup is a separate, retained copy typically stored independently and created on a schedule. A snapshot protects you against negative changes to your system becoming permanent, whereas a backup protects you from losing the system entirely. A snapshot is useful for quickly reversing unwanted changes, while a backup is designed to protect against data loss or loss of the original system.A backup is typically kept separately from the system it protects, while a snapshot is often kept on the system it protects.
```

**Analysis Question 3.** Your room was reserved for you rather than created by you. What does that tell you about how cloud access is usually handed out in a real organization, and why would an employer prefer that model? *(Minimum 2 sentences.)*

```
I think that in a real organization, VM/cloud rooms are created and reserved for employees rather than created by the employees themselves because it is easier and simpler for every employee to start from the same known-good machine. An employer would likely prefer that model because it gives the organization greater control over configuration, security, software, and access. If an issue occurs, it can be reproduced in a standardized environment, making it easier to diagnose and fix. Standardization also reduces the number of different configurations the organization has to support.
```

---

## Submission Checklist

- [x] VM started from My Lab Environment and confirmed **Running** (Part A, Step 1)

- [x] Signed in through Bastion as `analyst` — no credentials recorded anywhere (Part A, Step 2)

- [x] `hostname`, `whoami`, and `pwd` run and outputs recorded (Part A, Steps 3–5)

- [x] Explained what each of the three outputs proves (Part B, Step 1)

- [x] `bastion-session.png` captured, address bar and login data cropped out, uploaded to `assets/screenshots/week-06/` (Part B, Step 2)

- [x] Standardized/golden image explained in your own words (Part C)

- [x] All three Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-06/labs/lab-01-claiming-your-room.md`

---

## GitHub Commit Subsection

1. Open **Week 6 → Lab 01: Claiming Your Room in Cloud Heights** in the Lab Portal.
2. Fill in the worksheet fields — they match this file, in the same order.
3. Connect your GitHub account if you haven't already, and select your portfolio repo.
4. Click **Submit to GitHub**. The Portal commits the completed file to `week-06/labs/lab-01-claiming-your-room.md`.
5. Upload `bastion-session.png` to `assets/screenshots/week-06/` in your repo before you submit.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
