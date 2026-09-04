# Week 6 Lab 05 — Layer Detective

**Student Name:** David Wright

**Date Completed:** 9/4/2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 6  
**Submission Path:** `week-06/labs/lab-05-layer-detective.md`

---

## Overview

**This is a SHORT lab — 20 to 30 minutes — and it needs no VM.** No Cloud Heights session, no simulator, no screenshot. This is a thinking lab: you take the evidence you have already collected in Weeks 5 and 6 and sort it into layers.

This is an **independent** lab.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | This worksheet only — nothing to start, nothing to connect to |
| Prerequisite | Week 5 labs and Week 6 Labs 01–04 |
| Screenshot | None required |

---

## Part A — The Seven-Row Table

Fill in every row. For the last column, name one **real thing you personally saw** in Weeks 5–6 that belongs at that layer.

| # | Layer name | One-line job | Real thing from Weeks 5–6 |
| --- | --- | --- | --- |
| 7 | Separate reachability from authentication | ssh | In Lab 2 from Week 6, I used the 'ssh' command to authenticate myself in the VM, and was prompted to enter a password. |
| 6 | Trace the path  | traceroute | In Lab 3 for Week 6, I used this command to trace the route from my machine to my desired destination. |
| 5 | Test the destination by IP or service  | ping/curl | I used this command in Lab 3 for Week 6 to test the destination by contacting my desired service. |
| 4 | Test the destination by name  | dig | I used this command in Lab 1 for Week  5 to get the IP address for the archive server. |
| 3 | Test a known-good target | ping | I entered this command to test the Grid Beacon, a known-good target, in Lab 3 for Week 6. |
| 2 | Read your route  | ip route | I entered this command in Lab 3 for Week 6 to check my own routing table. |
| 1 | Check yourself  | ip addr | I entered this command in Lab 3 for Week 6 to check my own address. |

---

## Part B — Case Files

For each case, name the layer where the problem lives, and name the evidence proving the layers **below** it were already working.

### Case File 1 — The Name That Went Nowhere

A hostname lookup fails, but pinging the machine's IP address directly succeeds.

Layer:

```
Layer 4
```

Evidence that the layers below were working:

```
If Layer 4 (Test the destination by name using the 'dig' command) is not working, and Layer 5 (Test the destination by IP or service with 'ping/curl') is, what is mostly likely happening is that the 3 bottom layers (check yourself with 'ip addr', read your route with 'ip route', test a known-good target with ping) are working properly. If a ping to a machine's IP address succeeds (Layer 5), that means that the user's machine has a valid IP address (Layer 1), there is an operational route to the destination (Layer 2), and a known-good target can successfully be pinged (Layer 3). The problem is with the hostname, even if it can be bypassed in favor of testing the destination by its IP address.
```

### Case File 2 — Permission Denied

`ssh` to a host returns `Permission denied` after a password prompt.

Layer:

```
Layer 7
```

Evidence that the layers below were working:

```
If the user was able to get to the service and be prompted for a password, that means that enough of the previous 6 layers worked for him to reach the service and request entry to begin with. The layers that succeeded were Layer 1 (his machine exists on the network), Layer 2 (a valid path to the host exists), and Layer 5 (the service accepted the connection and presented an authentication prompt). Layers 3, 4, and 6 were not necessarily relevant for this process. When the user could not authenticate (or did not have authorization to log in), Layer 7 failed.
```

### Case File 3 — The Cable Story

A machine reports no link on its interface and has no address at all.

Layer:

```
Layer 1
```

Evidence and reasoning:

```
If a machine does not have a usable IP address, then you can't even establish its presence on the network, and it has failed at Layer 1. Therefore, it is impossible to test any of the higher layers.
```

### Case File 4 — Ping Works, The Page Does Not

`ping` to a server succeeds, but `curl http://<that server>` returns nothing useful.

Layer:

```
Layer 5
```

Evidence that the layers below were working:

```
Since a 'ping' to the server succeeded but a 'curl' to the server did not, it proved that Layers 1 and 2 were working properly. The machine has a valid IP address on the network (Layer 1), and a valid path to the server exists (Layer 2). Layers 3 and 4 are not relevant to this issue.
```

### Case File 5 — Wrong Neighbourhood

A machine has an address, but its default route points somewhere that cannot forward its traffic.

Layer:

```
Layer 2
```

Evidence and reasoning:

```
If a machine has a valid IP address but a default route that points somewhere that cannot forward its traffic, there is a failure at Layer 2. Having a valid IP address on the network clears Layer 1, but if it does not have a default route that gives it a way out, Layer 2 has failed.
```

---

## Part C — The Silent Gateway Case

In Lab 03 the Azure default gateway did not answer your ping. However, your VM had a valid default route configured, and your local communication with the Grid Beacon — the ping replies, the HTTP banner, and `TRACE ID: CF-NET-0604` — succeeded.

A failed gateway ping is one piece of evidence — not automatically proof of a gateway or network failure. But the evidence you weigh against it has to be the right kind of evidence.

The Grid Beacon at `10.60.6.4` sits on the same local subnet as your VM (`10.60.6.0/26`). Reaching it proves **local-subnet connectivity** — that traffic never crosses the default gateway, so beacon success alone cannot prove the gateway forwarded anything. Your `ip route` output proves a **default route is configured** — your VM knows where it intends to send non-local traffic — but it does not prove the gateway forwarded that traffic. The evidence that demonstrates the **default path is functioning** is successful communication with a destination outside `10.60.6.0/26`, such as the outbound internet access through NAT that you examined in Lab 04.

### Step 1 — Rule on the Case

Is the failed gateway ping enough evidence to declare a network-layer failure? Explain your answer using the other evidence you collected. In your response, distinguish between:

- evidence that proves **local-subnet connectivity**
- evidence that proves a **default route is configured**
- evidence that supports **successful off-subnet connectivity**

```
A failed gateway ping is not enough evidence to declare a network-layer failure, as the other pieces of evidence seem to point to the network being healthy. Reaching the Grid Beacon proves local-subnet connectivity, as the machine successfully reached a destination on the same subnet (but the traffic never crosses the default gateway, so that does not prove that the gateway forwarded anything). The 'ip route' output proves that a default route is configured (but does not prove the gateway forwarded the traffic). When the machine successfully communicated with a destination outside of the subnet, that proved that the default path (and therefore the gateway) is functioning correctly.
```

### Step 2 — Name the Correct Conclusion

For each of these four results, state what it actually proves: the Grid Beacon at `10.60.6.4` answering, the default route shown by `ip route`, a successful connection to a destination outside your local subnet, and the gateway's failed ping. Then state the rule you would give a junior colleague about the difference between an observation ("the gateway did not answer my ICMP probe") and a diagnosis ("the gateway is broken"):

```
When the Grid Beacon succesfully answered the ping, it proved local-subnet connectivity. When 'ip route' showed that a default route was configured, it proved that the VM knows where to send non-local traffic. When the machine successfully communicated with a destination outside of the subnet, it proved that the default path is functioning properly. Therefore, the failed ping does not really prove anything, as the network seems to be perfectly healthy. The gateway not answering the ICMP probe is one isolated observation, and does not prove a diagnosis (particularly not "the gateway is broken"). What is most likely is that the gateway is not configured to respond to ICMP requests, which is common with gateways (particularly those in Azure).
```

---

## Part D — Two Models, One Job

The OSI model has seven layers. The practical TCP/IP model most engineers speak day to day has four or five.

### Step 1 — Map Them

Briefly show how the seven OSI layers collapse into the practical model:

```
The OSI model has seven layers: 

1. Physical
2. Data Link
3. Network
4. Transport
5. Session
6. Presentation
7. Application

The practical TCP/IP model has five layers: 

1. Physical
2. Data Link
3. Network
4. Transport
5. Application

In the TCP/IP model, the Session and Presentation layers from the OSI model are collapsed into the Application layer.
```

### Step 2 — When Each Is Useful

Explain when the seven-layer vocabulary helps and when the practical model is the better tool:

```
The OSI model is better for some instances, and the TCP/IP model is more beneficial for others.The TCP/IP model is better for real-world applications, due to its flexibility and lower overhead. The OSI model is the superior choice when it comes to work that is highly structured and has strict boundaries, such as teaching and learning network concepts (the more cleanly each step of communication is separated, the easier it is to pinpoint a problem when it arises).
```

---

## Analysis Questions

**Analysis Question 1.** Explain the Ladder Rule using layer language. What does "test the near thing first" mean when the rungs are layers? *(Minimum 3 sentences.)*

```
The Ladder Rule is a structured roadmap to troubleshoot a network one layer at time, starting with your own machine and working your way outward. "Test the near thing first" means that you start by testing the layer closest to you, and the move on to the layer one step further out, and then to the layer one step further out from that one until you have discovere the problem. The first and nearest layer that you would always test is your own machine by confirming that it has a valid IP address.
```

**Analysis Question 2.** Why is "which layer is this?" a faster question than "what is broken?" when you are under pressure? *(Minimum 3 sentences.)*

```
"Which layer is this?" is a faster question than "what is broken?" when you are under pressure to fix a problem because the former question is much more specific than the latter. The latter question is merely a verdict, while the former question examines each piece of evidence and associates it with its correct layer, so every specific fact is clear and streamlined. This makes it more likely that you will get an accurate verdict, and therefore you will be better equipped to solve the actual problem (because you have a more definite idea of what it is).
```

**Analysis Question 3.** Pick one case file from Part B and describe the very next command you would run to confirm your ruling, and what result would change your mind. *(Minimum 2 sentences.)*

```
If a machine had a valid IP address but could not route raffic, the next command I would run would be a ping to a known-good target. If the ping to the known-good target failed, it would likely confirm that there was not a valid route. If the ping to the known-good target succeeded, then it would confirm that there was a valid route (even if it is not the default route).
```

---

## Submission Checklist

- [x] All seven rows of the OSI table completed with a real Week 5–6 anchor each (Part A)

- [x] All five case files given a layer and supporting evidence (Part B)

- [x] Silent gateway case ruled on correctly (Part C)

- [x] OSI vs. practical TCP/IP model compared (Part D)

- [x] All three Analysis Questions answered (minimum sentence counts met)

- [x] No screenshot required for this lab

- [x] This file is committed to your portfolio repo at `week-06/labs/lab-05-layer-detective.md`

---

## GitHub Commit Subsection

1. Open **Week 6 → Lab 05: Layer Detective** in the Lab Portal.
2. Fill in the worksheet fields.
3. Click **Submit to GitHub** — the Portal commits to `week-06/labs/lab-05-layer-detective.md`.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
