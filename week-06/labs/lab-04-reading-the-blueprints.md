# Week 6 Lab 04 — Reading the Blueprints

**Student Name:** David Wright

**Date Completed:** 9/5/2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 6  
**Submission Path:** `week-06/labs/lab-04-reading-the-blueprints.md`

---

> ### 🔒 Cloud Heights Security Rule
> Your Bastion link and Cloud Heights password are **private access credentials**. Never paste either into a worksheet, screenshot, GitHub repository, Circle post, or chat message. When taking screenshots, crop out the browser address bar and all login information.

---

## Overview

**This is a SHORT lab — 15 to 20 minutes.** It is deliberately small. You already have the commands; this lab is about matching a drawing to reality.

The **Cloud Heights Network Blueprint** is displayed at the top of this lab page in the portal. Everything you write about the network's architecture comes from that blueprint or from your own machine — never from a guess.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | Cloud Heights — live Ubuntu 22.04 VM, reached through Azure Bastion |
| Source of truth | The Cloud Heights Network Blueprint shown at the top of this lab page |
| Commands used | `ip addr`, `ip route` |
| Known value | Student subnet: **`10.60.6.0/26`** |

---

## Part A — Read the Drawing

### Step 1 — Record the Architecture Values

From the blueprint at the top of this page, record each value **exactly as drawn**. If a value is not shown on the blueprint, write "not shown on blueprint" — do not guess.

| Item | Value from the blueprint |
| --- | --- |
| VNet name | vnet-cf-labs |
| VNet address space | 10.60.6.0/24 |
| Student subnet range | 10.60.6.1-10.60.6.63 |

---

## Part B — Verify Against Your Own Machine

### Step 1 — Confirm Your Address Lives in the Subnet

Run `ip addr` and find your private IPv4 address.

Command and output:

```
Command: ip addr

Output: 

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 7c:ed:8d:c9:bf:1f brd ff:ff:ff:ff:ff:ff
    inet 10.60.6.37/26 metric 100 brd 10.60.6.63 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::7eed:8dff:fec9:bf1f/64 scope link 
       valid_lft forever preferred_lft forever
3: enP43438s1: <BROADCAST,MULTICAST,SLAVE,UP,LOWER_UP> mtu 1500 qdisc mq master eth0 state UP group default qlen 1000
    link/ether 7c:ed:8d:c9:bf:1f brd ff:ff:ff:ff:ff:ff
    altname enP43438p0s2
```

Your private IP:

```
10.60.6.37
```

Explain how you know your address falls inside `10.60.6.0/26` — what range does that prefix actually cover:

```
The range that the /26 prefix covers for my address is 10.60.6.0-10.60.6.63. Therefore, my address (10.60.6.37) falls within that range.
```

### Step 2 — Confirm Route Behaviour

Run `ip route`.

Command and output:

```
Command: ip route

Output:
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 7c:ed:8d:c9:bf:1f brd ff:ff:ff:ff:ff:ff
    inet 10.60.6.37/26 metric 100 brd 10.60.6.63 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::7eed:8dff:fec9:bf1f/64 scope link 
       valid_lft forever preferred_lft forever
3: enP43438s1: <BROADCAST,MULTICAST,SLAVE,UP,LOWER_UP> mtu 1500 qdisc mq master eth0 state UP group default qlen 1000
    link/ether 7c:ed:8d:c9:bf:1f brd ff:ff:ff:ff:ff:ff
    altname enP43438p0s2
analyst@cf-student-18:~$ ^C
analyst@cf-student-18:~$ ip route
default via 10.60.6.1 dev eth0 proto dhcp src 10.60.6.37 metric 100 
10.60.6.0/26 dev eth0 proto kernel scope link src 10.60.6.37 metric 100 
10.60.6.1 dev eth0 proto dhcp scope link src 10.60.6.37 metric 100 
168.63.129.16 via 10.60.6.1 dev eth0 proto dhcp src 10.60.6.37 metric 100 
169.254.169.254 via 10.60.6.1 dev eth0 proto dhcp src 10.60.6.37 metric 100 

```

What the default route tells you about traffic that is not destined for your own subnet:

```
The default route tells me that my machine sends traffic not destined for my own subnet to the default gateway (10.60.6.1).
```

### Step 3 — Capture Your Evidence

**Required filename:** `blueprint-verified.png`

This must be **your own `ip addr` and `ip route` output** — not a re-screenshot of the blueprint. Crop out the address bar and any login information.

---

## Part C — How Traffic Actually Moves

### Step 1 — No Public IP

Your VM has a private address and **no public IP**. Explain what that means for who can reach it directly from the internet:

```
When a VM has a private IP address and no public IP address, nobody can reach it directly from the internet using the private IP address. In order to reach my VM, a user on the internet could go to Azure Bastion as a secure entry point into the VNet, which would allow connection to the VM using its private IP address.
```

### Step 2 — Outbound vs. Inbound

Outbound internet traffic from your VM leaves through address **translation (NAT)**. Inbound access for you arrives through **Azure Bastion**, not through a public address on the VM.

Explain both directions in your own words:

```
Inbound internet traffic to your VM can arrive via Azure Bastion, which is a secure, managed entry point (a proverbial guarded front desk) into your VNet (the proverbial building). Azure Bastion can allow inbound management traffic to access your VM (hotel room) using its private IP address (room number). Outbound internet traffic travels from your VM through NAT at the proverbial loading dock, and the platform swaps your VM's private IP address for a shared public IP address on the way out.
```

### Step 3 — The Guard Post You Do Not Touch Yet

Each student machine sits behind its own **network security group** — a per-student guard post that decides what traffic is allowed in.

**In Week 6 you do not configure it.** Week 7 is when you take control of those rules.

Write one sentence naming what the guard post does and one sentence stating what you are *not* doing with it this week:

```
A guard post (Azure Bastion) controls the entrance of the proverbial building (VNet). If it decides that you are authorized to enter, it provides a secure path to the VM (room) inside the building.
```

---

## Analysis Questions

**Analysis Question 1.** Why would an organization put every student machine in one small subnet instead of giving each machine a public address? *(Minimum 3 sentences.)*

```
There are several benefits to an organization for putting every student machine into one small subnet rather than giving each machine a public address. If every student machine had a public IP address, they would all be reachable from the internet and thus all be exposed endpoints. Each address would represent an individual exposed endpoint (and thus an increase to the network's attack surface). Due to there being many individually exposed endpoints, each endpoint would need to be secured and monitored, thus making management of the network much more complicated. Putting every student machine into one small subnet limits public exposure, reduces the attack surface, and enables easier centralized management.
```

**Analysis Question 2.** Segmentation means separating a network into parts that cannot freely reach each other. Give one concrete benefit of segmentation during a security incident. *(Minimum 3 sentences.)*

```
One significant benefit of segmentation is that if an attacker gains access to a network, he/she does not automatically have access to the entire network. If a network is segmented, an attacker is more likely to be confined to one area and unable to access other areas. Therefore, the amount and scope of damage he/she can do is mitigated, as he/she can only damage one part of the network, as opposed to multiple parts of the network.
```

**Analysis Question 3.** A diagram and a live machine disagree about an address range. Which do you trust, what do you do next, and why? *(Minimum 2 sentences.)*

```
If a diagram and a live machine disagree about an address range, I would trust the live machine. The live machine represents observed reality, while the diagram represents documentation-it is better to trust observed reality over documentation when they disagree. I would accept the live configuration as the baseline for the rest of my investigation. I would also make a note of the discrepancy between the live VM and documentation, and investigate the reason for that later.
```

---

## Submission Checklist

- [x] VNet name, address space, and subnet range recorded from the blueprint (Part A)

- [x] `ip addr` run and own private IP confirmed inside `10.60.6.0/26` (Part B, Step 1)

- [x] `ip route` run and default route behaviour explained (Part B, Step 2)

- [x] `blueprint-verified.png` captured from your own terminal, cropped, uploaded to `assets/screenshots/week-06/` (Part B, Step 3)

- [x] Private address / NAT / Bastion explained (Part C, Steps 1–2)

- [x] Per-student guard post identified — and explicitly not configured this week (Part C, Step 3)

- [x] All three Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-06/labs/lab-04-reading-the-blueprints.md`

---

## GitHub Commit Subsection

1. Open **Week 6 → Lab 04: Reading the Blueprints** in the Lab Portal.
2. Fill in the worksheet fields and upload `blueprint-verified.png` to `assets/screenshots/week-06/`.
3. Click **Submit to GitHub** — the Portal commits to `week-06/labs/lab-04-reading-the-blueprints.md`.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
