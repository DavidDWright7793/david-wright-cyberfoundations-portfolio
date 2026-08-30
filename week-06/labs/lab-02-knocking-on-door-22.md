# Week 6 Lab 02 — Knocking on Door 22

**Student Name:** David Wright

**Date Completed:** 8/30/2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 6  
**Submission Path:** `week-06/labs/lab-02-knocking-on-door-22.md`

---

> ### 🔒 Cloud Heights Security Rule
> Your Bastion link and Cloud Heights password are **private access credentials**. Never paste either into a worksheet, screenshot, GitHub repository, Circle post, or chat message. When taking screenshots, crop out the browser address bar and all login information.

---

## Overview

Week 5 told you SSH is how administrators reach a machine over the network, and that it knocks on **port 22**. This week you knock yourself. You are already inside Cloud Heights through Bastion — now you will open a second, nested SSH session from your machine *to itself* and watch every step of what SSH does before it lets you in.

Starts **guided**, finishes **independent**. Expect 30–40 minutes.

**This lab uses password authentication only.** SSH keys are Week 8. Do not go looking for them yet.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | Cloud Heights — live Ubuntu 22.04 VM, reached through Azure Bastion |
| Username | `analyst` |
| Password | Provided separately. Never typed into this worksheet. |
| Commands used | `ssh`, `whoami`, `hostname`, `pwd`, `exit` |
| Prerequisite | Week 6 Lab 01 completed |

**Before you start:** open **My Lab Environment**, start your VM if needed, wait for **Running**, then open Cloud Heights.

---

## Part A — Two Ways Into the Same Room

### Step 1 — Name the Path You Already Used

You reached Cloud Heights through a browser session. Something else handled the network hop for you.

Describe, in your own words, what the Bastion/browser path did on your behalf:

```
The Bastion/Browser path led me to a managed entry point to Bastion in my browser. Bastion handled the network connection to the VM on my behalf, after authenticating and authorizing my access, without requiring the VM to have a public IP address.
```

### Step 2 — Predict the Manual Path

You are about to type an SSH command by hand. Before you run it, write what you expect to happen and what you expect to be asked for:

```
When I type an SSH command, I would expect Bastion to establish the connection to the VM from inside the Azure virtual network. After that, I would expect to be asked for an SSH username/password or private key.
```

---

## Part B — Knocking

### Step 1 — Run the SSH Command

In your Cloud Heights terminal, run:
```
ssh analyst@localhost
```

After you press Enter, SSH may show one of two valid responses.

- If this SSH client has not recorded `localhost` before, you may receive a **first-connection host fingerprint prompt**.
- If `localhost` is already recorded as a known host, SSH may skip that prompt and take you **directly to password authentication**.

Both are valid. Continue with the instructions that match what you see.

### Step 2 — Observe the SSH Connection

The first time SSH connects to an unfamiliar host, it may display the host's **fingerprint** and ask whether you want to continue connecting.

If the host is already recorded in your SSH `known_hosts` file, SSH may skip this confirmation and proceed directly to authentication.

**Do not reset or delete SSH trust information just to make the first-connection prompt appear.**

**If you see the fingerprint prompt:** stop and read it, record it below, answer the question that follows, and then type `yes` when you are ready to continue. A fingerprint is **not** a credential — it is a public identifier of the machine, so it is safe to record.

**If you do not see the fingerprint prompt:** this is okay. It means SSH already recognises `localhost` as a known host in this environment. Write `Host already known — fingerprint prompt not displayed.` below and continue to Step 3. You lose no credit for this.

Record what SSH showed you — paste the first-connection prompt, or write `Host already known — fingerprint prompt not displayed.`:

```
Host already known - fingerprint prompt not displayed.
```

Why does SSH verify a host's identity when connecting to an unfamiliar system? If you received the first-connection prompt, also explain why it was reasonable to continue in this controlled Cloud Heights lab environment:

```
I was willing to answer 'yes' here because every SSH connection has two sides with two different jobs. My side, as the client, is knocking on the proverbial door, and the server, the other side, is answering and deciding whether or not to let me in. Also, getting to a machine and getting into a machine are two different issues.
```

### Step 3 — Enter Your Password

> ### ⚠️ PASSWORD INPUT WILL BE INVISIBLE
> When SSH asks for the `analyst` password, type or paste the password and press Enter.
>
> Linux does not display password input.
>
> You will **NOT** see:
> - letters or numbers
> - dots
> - asterisks
> - the cursor moving as characters are entered
>
> This is normal.
>
> The terminal may look like nothing is happening even though it is accepting the password.
>
> Enter the password once, press Enter once, and wait for SSH to respond.
>
> If clipboard paste does not work in your browser/Bastion terminal, type the password manually.

If you saw the fingerprint prompt, type `yes` first. Then enter your password at the password prompt.

**Troubleshooting.** If you get `Permission denied`, do not repeatedly retry credentials — capture the error and contact your instructor or post in the Lab Troubleshooting space. If you enter the password, press Enter, wait several seconds, and get neither a new prompt nor an error, capture the entire terminal state for troubleshooting. Do not restart the whole lab on your own.

What did the screen show while you typed:

```
The screen did not show anything significant while I typed.
```

### Step 4 — Prove You Are in the Nested Session

Inside the new session run each of these and record the output:
```
whoami
```

```
analyst
```

```
hostname
```

```
cf-student-18
```

```
pwd
```

```
/home/analyst
```

### Step 5 — Notice the Prompt

Compare the prompt now to the prompt before you ran `ssh`. Describe anything that changed and anything that looks identical, and explain why it looks that way given where you connected to:

```
Almost everything about the prompt before running 'ssh' and the prompt after running 'ssh' is identical, except for a few little differences (cue Pulp Fiction). In the pre-SSH prompt, it said that 135 processes were running. In the post-SSH prompt, it said that there were 136 processes running. Also, the pre-SSH prompt shows 0 users logged in, while the post-SSH prompt shows 1 user logged in. The reason for these changes was that I logged into another system when I ran 'ssh', and thus got another process running.
```

### Step 6 — Capture Your Evidence

Screenshot your terminal showing the SSH connection activity. **Either** valid state is accepted:

- **State A** — a screenshot showing the SSH **first-connection / fingerprint prompt** (and the successful session), **or**
- **State B** — a screenshot showing the SSH **authentication / successful login** state when `localhost` was already a known host.

Your screenshot must show that you performed the SSH connection. You are not penalised if the fingerprint prompt was never generated.

**Required filename:** `ssh-first-connection.png` (filename kept for submission compatibility — its contents may show either state)

**Crop rules.** No Bastion URL, no address bar, no password field, no login screen. The fingerprint text, if present, is fine.

### Step 7 — Leave

Run:
```
exit
```
What did the prompt look like after exiting, and how do you know you are back in the original session:

```
The prompt said 'logout', and then 'Connection to localhost closed'. That indicated that the SSH connection to localhost was terminated, and I was back in the original session.
```

---

## Part C — The Deliberate Failure (Independent)

### Step 1 — Knock With the Wrong Name

Run an SSH command to `localhost` using a username that does not exist on this machine — for example `ssh notauser@localhost`. Enter anything at the password prompt.

Command you ran:

```
ssh notauser@localhost
```

Output:

```
Permission denied, please try again.
```

### Step 2 — Read the Failure Correctly

`Permission denied` is a **failure of authentication**, not a failure of the network.

Explain what the network and SSH already had to do successfully in order for you to be told "permission denied" at all:

```
The network first had to successfully get me to the "door", where the name has to resolve and the path has to exist. Otherwise, I could not get to the port at all. SSH has to determine that a service is running and listening on the other side of the "door" (port) in order to make a decision to allow or deny me permission to enter.
```

---

## Analysis Questions

**Analysis Question 1.** Distinguish *reach* from *authentication*. Which one had already succeeded when you saw a password prompt, and how do you know? *(Minimum 3 sentences.)*

```
Reach and authentication are two different concepts. Reach is arriving at the door-this means that the name resolved, the path exists, and something is listening on port 22. Authentication is proving that you are an account that the machine will accept. In other words, reach is what allows you to arrive at the door, and authentication is what allows you to walk through the door. Reach has succeeded when you see a password prompt, as you would never get to that prompt without arriving there and having someone on the other side listening to begin with.
```

**Analysis Question 2.** SSH records a host's identity so it can warn you if that identity ever changes. Describe a situation where accepting a host fingerprint without thinking — or ignoring a changed-host warning — would be a real problem. *(Minimum 3 sentences.)*

```
A situation where you ignore a changed-host warning on a machine could cause you to enter and interact with a machine that you did not intend to enter or interact with. If you made adjustments on the wrong machine without thinking, that could cause frustrating consequences in many forms. Additionally, the changes you would try to make on the intended machine would not take effect, and you would be unaware as to why they would not be taking effect. In short, ignoring a changed-host warning and making changes to a different machine than intended can create a great deal of frustration and confusion for users of both machines, yourself included.
```

**Analysis Question 3.** What changed and what stayed the same when you moved from the outer session into the nested SSH session, and why? *(Minimum 2 sentences.)*

```
When I moved from the outer session into the nested SSH session in my VM, the original environment stayed the same-the outer session was still there underneath the SSH connection. However, once the SSH connection was established, one additional user/session was logged onto the destination VM, and one additional process was running. Also, the shell was then running on the destination VM, and any commands I entered would affect that VM.
```

**Analysis Question 4.** A colleague says "SSH is broken, I got permission denied." Using only what you learned in this lab, what would you tell them is already working, and what would you check next? *(Minimum 3 sentences.)*

```
I would tell my colleague that reachability of the SSH service is most likely not the issue. If they got a "permission denied" message, the hostname resolves, the destination is reachable, and port 22 is listening and responding. The problem appears to be at login, where the SSH service decides to allow the user into the system. I would check authentication and authorization at login as the next troubleshooting step, as there could be a few different issues with that that could result in the user being denied permission to enter.
```

---

## Submission Checklist

- [x] Bastion path vs. manual SSH path described (Part A)

- [x] `ssh analyst@localhost` run and the SSH response recorded — fingerprint prompt **or** "host already known" (Part B, Steps 1–2)

- [x] Password entered; non-echoing input observed and described (Part B, Step 3)

- [x] `whoami`, `hostname`, `pwd` run inside the nested session (Part B, Step 4)

- [x] Prompt change described (Part B, Step 5)

- [x] `ssh-first-connection.png` captured (fingerprint prompt **or** authentication/login state), cropped, uploaded to `assets/screenshots/week-06/` (Part B, Step 6)

- [x] Session exited cleanly (Part B, Step 7)

- [x] Bad-username test run and `Permission denied` output recorded (Part C)

- [x] All four Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-06/labs/lab-02-knocking-on-door-22.md`

---

## GitHub Commit Subsection

1. Open **Week 6 → Lab 02: Knocking on Door 22** in the Lab Portal.
2. Fill in the worksheet fields and upload `ssh-first-connection.png` to `assets/screenshots/week-06/`.
3. Click **Submit to GitHub** — the Portal commits to `week-06/labs/lab-02-knocking-on-door-22.md`.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
