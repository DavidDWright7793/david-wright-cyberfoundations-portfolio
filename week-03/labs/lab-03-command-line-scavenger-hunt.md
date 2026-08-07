# Week 3 Lab 03 — Command Line Scavenger Hunt (CLI Simulator)

**Student Name:** David Wright

**Date Completed:** 8/3/2026

**Module:** 1 — Digital Infrastructure & CLI | **Week:** 3  
**Submission Path:** `week-03/labs/lab-03-command-line-scavenger-hunt.md`

---

## Overview

Labs 01 and 02 walked you through each command step by step. This lab is Week 3's wrap-up challenge: a deeper, more independent folder structure with three hidden files to track down, using the navigating and reading commands from Lessons 3A/3B, the creating and organizing commands from Lesson 3C, and your own judgment about when to ask for help. There's less hand-holding here on purpose — this is your chance to prove to yourself that the blinking cursor from the start of Lesson 3A doesn't intimidate you anymore.

**Nothing here can break anything real.** Same consequence-free CLI Simulator as Labs 01 and 02. Getting "lost" in the folder tree costs you nothing but a few extra `cd` moves.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | CyberFoundations CLI Simulator (browser-based, inside the Lab Portal) |
| Shell | Your choice — bash or PowerShell |
| Prerequisite | Labs 01 and 02 completed |

**Before you start:** log into the Lab Portal, open **Week 3 → CLI Simulator**, and load the **"Foundry District Archive Room"** scenario. This tree goes several folders deeper than Labs 01 and 02, and includes a few similarly-named folders on purpose — read carefully before you `cd` into anything.

---

## Part A — The Hunt

Find all three of the following, hidden at different depths in the Archive Room tree:

- A file related to a **shift log**
- A file related to a **maintenance note**
- A file related to a **supply inventory**

For each one, use `pwd`/`Get-Location` and `ls`/`dir` as many times as you need while you search, then record the **full path** once you find it.

Shift log file — full path once found:

```
 /home/archivist/operations/ops-log>
```

Maintenance note file — full path once found:

```
 /home/archivist/records/records-2025> 
```

Supply inventory file — full path once found:

```
 /home/archivist/records/records-2024> 
```

---

## Part B — Read and Report

For each of the three files you found in Part A, use `cat`/`type` to read it and record what it says.

Shift log contents:

```
Shift Log - Foundry District Archive Room
07:00 - Archive opened, no incidents overnight.
15:00 - Routine filing complete.
```

Maintenance note contents:

```
Maintenance Note - Conveyor belt 3 serviced, next check due in 90 days.
```

Supply inventory contents:

```
Supply Inventory - Q4 2024
Gloves - 400 units
Masks - 250 units
Tape - 60 rolls
```

---

## Part C — Organize Your Findings

Now that you've located and read all three files, clean up after yourself the way a professional would — don't leave your findings scattered across the tree.

### Step 1 — Create a Sorted-Findings Folder

Create a new folder called `sorted-findings` in your home directory.

Command you ran:

```
mkdir sorted-findings
```

### Step 2 — Move All Three Files Into It

Move the shift log, maintenance note, and supply inventory files — the same three you found in Part A — into `sorted-findings`.

Commands you ran:

```
mv operations/ops-log/shift-log.txt sorted-findings/
mv records/records-2025/maintenance-note.txt sorted-findings/
mv records/records-2024/supply-inventory.txt sorted-findings/
```

### Step 3 — Confirm the Move

List the contents of `sorted-findings` to confirm all three files are now there.

Command you ran:

```
ls sorted-findings
```

Output:

```
maintenance-note.txt  shift-log.txt  supply-inventory.txt
```

---

## Part D — When You Get Stuck

At some point in the Archive Room, you'll likely run across a command or folder name you don't immediately recognize.

### Step 1 — Ask the Terminal

When that happens, use `--help`, `man`, or `Get-Help` instead of guessing. Record what you looked up and what you learned.

Command or term you looked up:

```
chmod
```

What the help text (or the folder's contents) told you:

```
The command 'chmod' changes the permissions (read, write, execute) on the file for the owner, groups, and users.
```

### Step 2 — Describe a Wrong Turn

Everyone takes at least one wrong turn in a tree this size. Describe one moment you ended up somewhere unexpected, and how you used `pwd`/`Get-Location` and `cd ..` to recover.

```
I made a few wrong turns during this exercise. I did turn into the ops-notes folder once, but when I realized it did not have any files of interest to my task, I used 'cd ..' to return to the previous folder.
```

---

## Analysis Questions

### Analysis Question 1

Which of the three files in Part A took the longest to find, and what was it about the tree's structure (depth, similarly-named folders, etc.) that made it harder?

```
I don't think any of the files in Part A took a particularly long time for me to find. However, I did take a wrong turn into ops-notes because I thought the shift log might be there due to the name of the folder. I quickly realized the shift log wasn't there, and turned back to the operations folder, then directed into the ops-log folder.
```

### Analysis Question 2

Compare how you felt starting this lab to how you felt at the very start of Lesson 3A, looking at a blank blinking cursor for the first time. What changed?

```
I had used PowerShell extensively during my coding bootcamp a couple years ago, so I was not entirely unfamiliar with it. However, it had been a while since I had actually used it, so I felt a bit rusty. I have been working my way through the Linux/SQL section of the Google Cybersecurity Certificate on Coursera, so that has refreshed my memory a bit and even taught me some new things. I am beginning to get more comfortable with PowerShell/Bash due to these lessons in CyberVisionaries and the Google Cybersecurity Certificate.
```

### Analysis Question 3

Week 4 moves from managing your own files to controlling who's allowed to do what to them — permissions — plus your first look at what a virtual machine is. Based on everything you've practiced this week, what's one thing you're curious about or looking forward to?

```
I am definitely curious about using virtual machines more extensively. I am very interested in learning more about the cloud, as I am interested in earning several certifications from Microsoft Azure and AWS, as well as cloud security certifications from SANS and ISC2.
```

---

## Submission Checklist

- [x] All three target files located, with full paths recorded (Part A)

- [x] All three target files read and their contents recorded (Part B)

- [x] `sorted-findings` folder created and all three files moved into it, confirmed with a listing (Part C)

- [x] At least one command or term looked up with `--help`/`man`/`Get-Help`, with what you learned recorded (Part D, Step 1)

- [x] One wrong-turn moment described, including how you recovered (Part D, Step 2 — minimum 2 sentences)

- [x] All three Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-03/labs/lab-03-command-line-scavenger-hunt.md`

---

## GitHub Commit Subsection

Same mechanism as Labs 01 and 02: fill out this lab's worksheet in the **CyberFoundations Lab Portal** (Week 3 → Lab 03) and click **Submit to GitHub** — the Portal commits the completed file to `week-03/labs/lab-03-command-line-scavenger-hunt.md` automatically. No manual typing or commit needed.

**📌 Optional:** a CLI Simulator session screenshot can be added the same way as Labs 01 and 02 — upload to `assets/screenshots/week-03/`, then right-click the uploaded image and choose **Copy image address**/**Copy Image Link** to embed it — but it isn't required and won't affect your grade.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
