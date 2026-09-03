# Week 6 Lab 03 — The Grid, For Real

**Student Name:** David Wright

**Date Completed:** 9/3/2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 6  
**Submission Path:** `week-06/labs/lab-03-the-grid-for-real.md`

---

> ### 🔒 Cloud Heights Security Rule
> Your Bastion link and Cloud Heights password are **private access credentials**. Never paste either into a worksheet, screenshot, GitHub repository, Circle post, or chat message. When taking screenshots, crop out the browser address bar and all login information.

---

## Overview

In Week 5 you ran `ip addr`, `ip route`, `ping`, and `traceroute` in a simulator that always behaved. Today you run the same toolkit against real cloud infrastructure that does **not** always behave the way the textbook implies — and you learn to tell "broken" apart from "normal."

This is an **independent** lab. It tells you what to accomplish; you choose the commands. Expect about 40 minutes.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | Cloud Heights — live Ubuntu 22.04 VM, reached through Azure Bastion |
| Commands used | `ip addr`, `ip route`, `ping`, `traceroute`, `curl` |
| Known-good target | **Grid Beacon — `10.60.6.4`** |
| Prerequisite | Week 6 Labs 01–02 |

---

## Part A — Where You Actually Are

### Step 1 — Read Your Own Address

Run the command that lists your interfaces and addresses.

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
3: enP32080s1: <BROADCAST,MULTICAST,SLAVE,UP,LOWER_UP> mtu 1500 qdisc mq master eth0 state UP group default qlen 1000
    link/ether 7c:ed:8d:c9:bf:1f brd ff:ff:ff:ff:ff:ff
    altname enP32080p0s2
```

Your private IPv4 address and prefix length:

```
Private IPv4 address and prefix length: 10.60.6.37/26
```

### Step 2 — Read Your Route

Run the command that shows the routing table.

Command and output:

```
Command: ip route

Output: 

default via 10.60.6.1 dev eth0 proto dhcp src 10.60.6.37 metric 100 
10.60.6.0/26 dev eth0 proto kernel scope link src 10.60.6.37 metric 100 
10.60.6.1 dev eth0 proto dhcp scope link src 10.60.6.37 metric 100 
168.63.129.16 via 10.60.6.1 dev eth0 proto dhcp src 10.60.6.37 metric 100 
169.254.169.254 via 10.60.6.1 dev eth0 proto dhcp src 10.60.6.37 metric 100 
```

Your default gateway:

```
Default Gateway: 10.60.6.1
```

### Step 3 — Compare to Week 5

Compare this live Ubuntu output to what the CLI Simulator produced in Week 5. What looks the same, what looks different, and what surprised you:

```
The live Ubuntu output from this lab was largely similar to the output from the CLI Simulator from Week 5, but there were a few differences. The format of the output from both weeks was the same, but there was much more of a quantity of output from the same commands in Week 6 than Week 5. One significant difference is that the prefix length for the private IPv4 address from the CLI Simulator output in the Week 5 exercise is shorter than that of the private IPv4 address from the live Ubuntu output for the Week 6 exercise. For Week 5, the prefix length of the private IPv4 address is /24, whereas it is /6 for Week 6.
```

---

## Part B — The Gateway That Does Not Answer

### Step 1 — Ping the Gateway

Ping the default gateway address you recorded. Let it run a few seconds, then stop it.

Command and output:

```
Command: ping 10.60.6.1

Output:

PING 10.60.6.1 (10.60.6.1) 56(84) bytes of data.

--- 10.60.6.1 ping statistics ---
24 packets transmitted, 0 received, 100% packet loss, time 23589ms

```

### Step 2 — Interpret It Correctly

You almost certainly got **no replies**. In Azure, the platform gateway commonly does not answer ICMP. This is **expected platform behaviour** and by itself proves nothing about whether your machine or network is broken.

Explain why "the gateway did not answer ping" is weak evidence:

```
"The gateway did not answer ping" can be evidence, but definitely does not prove in and of itself that your machine or network is broken. The reason is that in Azure, the default gateway commonly does not answer ICMP even when the network is perfectly healthy. In fact, many healthy machines and most cloud gateways are configured to ignore pings entirely. An analogy is that if a neighbor knocks on my door and I do not answer it because I do not want to deal with him-just because I am not answering the door does not mean that I am not home.
```

---

## Part C — The Known-Good Target

The **Grid Beacon** at `10.60.6.4` is a machine that is known to be up and known to answer. When your first probe fails, you test against something known-good before you conclude anything.

### Step 1 — Ping the Beacon

```
ping 10.60.6.4
```
Output:

```
Output: 

64 bytes from 10.60.6.4: icmp_seq=1 ttl=64 time=1.12 ms
64 bytes from 10.60.6.4: icmp_seq=2 ttl=64 time=1.09 ms
64 bytes from 10.60.6.4: icmp_seq=3 ttl=64 time=1.14 ms
64 bytes from 10.60.6.4: icmp_seq=4 ttl=64 time=1.25 ms
64 bytes from 10.60.6.4: icmp_seq=5 ttl=64 time=1.12 ms
64 bytes from 10.60.6.4: icmp_seq=6 ttl=64 time=1.09 ms
64 bytes from 10.60.6.4: icmp_seq=7 ttl=64 time=1.09 ms
64 bytes from 10.60.6.4: icmp_seq=8 ttl=64 time=1.11 ms
64 bytes from 10.60.6.4: icmp_seq=9 ttl=64 time=1.01 ms

--- 10.60.6.4 ping statistics ---
9 packets transmitted, 9 received, 0% packet loss, time 8010ms
rtt min/avg/max/mdev = 1.014/1.114/1.254/0.059 ms
```

### Step 2 — Trace the Path

```
traceroute 10.60.6.4
```
Output:

```
Output:

traceroute to 10.60.6.4 (10.60.6.4), 30 hops max, 60 byte packets
 1  * * *
 2  grid-beacon.internal.cloudapp.net (10.60.6.4)  1.509 ms * *
```

### Step 3 — Ask the Application

```
curl http://10.60.6.4
```
Output:

```
Output: 

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GRID BEACON | CVI CyberFoundations</title>
    <style>
        body {
            background: #071426;
            color: #d9f7ef;
            font-family: monospace;
            max-width: 850px;
            margin: 80px auto;
            padding: 30px;
        }
        .beacon {
            border: 1px solid #31d6a6;
            padding: 35px;
        }
        h1 { color: #31d6a6; }
        .label { color: #8ca8ff; }
        .status { color: #31d6a6; }
        .classified {
            margin-top: 30px;
            border-top: 1px solid #31445e;
            padding-top: 20px;
        }
    </style>
</head>
<body>
<div class="beacon">

    <h1>GRID BEACON</h1>

    <p><span class="label">NODE:</span> grid-beacon</p>
    <p><span class="label">NETWORK:</span> CVI Training Grid</p>
    <p><span class="label">STATUS:</span>
       <span class="status">ONLINE</span></p>

    <p>
        Network beacon established.<br>
        If you reached this node, your route is operational.
    </p>

    <div class="classified">
        <p>INVESTIGATION CHECKPOINT</p>

        <p>
            Observe the path that brought you here.
m           The destination is only part of the story.
        </p>

        <p>TRACE ID: CF-NET-0604</p>
    </div>

</div>
</body>
</html>
            

```

> ### ⚠️ Grid Beacon not responding?
> The Grid Beacon is shared course infrastructure and should normally be available. First, confirm your Cloud Heights VM shows **Running** and that you completed the preceding network checks. Then retry the command once after a minute or two.
>
> If the Grid Beacon still does not respond, **stop this part of the lab and contact your instructor.** Record that the shared service was unavailable; do not treat the result as evidence that your VM or your work is incorrect.
>
> Do not change networking, NSGs, firewall rules, routes, DNS, or any Azure settings to try to reach the beacon.
>
> *Instructor note: a confirmed Grid Beacon outage is an environment issue, not a student error. Affected students may complete this portion of Lab 03 after the service is restored, with no penalty.*

### Step 4 — Record the Application Evidence

The beacon returns a banner and a trace ID. Record exactly what you received:

```
Beacon Banner: GRID BEACON

Trace ID: CF-NET-0604
```

Explain the difference between what the `ping` proved and what the `curl` proved:

```
The 'ping' proved that the network was reachable. The 'curl' proved that the web service was reachable and able to respond. The 'ping' command answered the question of "Can I reach the host at the network level?", and the 'curl' command answered the question of "Can I communicate with the specific web service running on that host?" Going back to the door analogy-'ping' is like "Can I go to my neighbor's door and knock on it?", while 'curl' is like "Is my neighbor there, and can I talk to him?".
```

### Step 5 — Capture Your Evidence

Two screenshots, both cropped to the terminal only:

**Required filename:** `vm-toolkit-live.png` — your `ip addr` and `ip route` output

**Required filename:** `beacon-reply.png` — your beacon ping/traceroute/curl evidence

---

## Part D — Rewrite the Ladder Rule

Week 5 taught the Ladder Rule: test the near thing before the far thing. Real infrastructure adds a wrinkle — a silent rung is not automatically a broken rung.

Rewrite the Ladder Rule in your own words so that it survives real cloud infrastructure. Your version must include both **route/path evidence** and **a known-good target**:

```
The Ladder Rule adapted for cloud environments is different from that of traditional network environments because it involves two additional steps to collect two additional pieces of evidence. The Ladder Rule, Cloud Edition includes seven rungs, worked outward, to collect seven pieces of evidence to help identiy the culprit. The seven rungs of the proverbial ladder are as follows: 1. check your own address (ip addr) 2. Read your route 3. Test a known-good target (ping) 4. Test the destination by name (dig) 5. Test the destination by IP or service (ping/curl) 6. Trace the path (traceroute) 7. Separate reachability from authentication, i.e. separate being able to reach the door to being able to get in the door.
```

---

## Analysis Questions

**Analysis Question 1.** Your ping to the gateway failed and your ping to the beacon succeeded. What does that pair of results, taken together, prove about your machine's networking? *(Minimum 3 sentences.)*

```
When a ping to the gateway fails and a ping to the beacon succeeds, the most likely conclusion is that the gateway is not configured to respond to ICMP, but the gateway is still routing traffic successfully. For a ping to successfully reach the beacon, it would need to be forwarded by the gateway (whether or not the gateway itself responds to ICMP). The successful png to the beacon proves that my machine has working IP connectivity to the beacon, and something is successfully forwarding traffic beyond the gateway. The best thing to investigate at that point is whether the gateway is configured to ignore ICMP, in order to avoid prematurely diagnosing the network with a problem.
```

**Analysis Question 2.** Why is `traceroute` useful even when `ping` already answered? What extra thing does it show you? *(Minimum 2 sentences.)*

```
The 'traceroute' command is useful even when 'ping' already answered because 'traceroute' shows how many hops traffic takes to get to its destination. The 'ping' command tells you if your destination responds, and the 'traceroute' command shows you how many hops traffic takes to reach its destination.
```

**Analysis Question 3.** A service is unreachable and ping to it succeeds. Where would you look next, and why is "the network is fine" an incomplete answer? *(Minimum 3 sentences.)*

```
If a service is unreachable and a ping to it succeeds, it means that you can reach the host, but you have not established that the specific service is available. The first troubleshooting step from there would be to identity the specific service/port you are trying to reach, and then testing that specific port. The 'curl' command would work especially well for this task. A successful ping only means that basic network connectivity is working, and does not tell you that the specific service is reachable.
```

**Analysis Question 4.** Something already controls what is allowed to reach your machine in Cloud Heights. If you could decide those rules, what would you want to allow, what would you want to block, and who in an organization should get to make that decision? *(Minimum 3 sentences.)*

```
If I could control what is allowed to reach my VM, I would utilize the concept of least privilege. I would only allow traffic that the VM needs to receive to perform its job responsiblities, and block everything else. The network/security teams should make the decision about what should be allowed or blocked on the VM, as they should know what the minimum amount of traffic the VM needs to receive to fulfill its function while avoiding unnecessary risk.
```

---

## Submission Checklist

- [x] `ip addr` output recorded and own private IP/prefix identified (Part A)

- [x] `ip route` output recorded and default gateway identified (Part A)

- [x] Live output compared to the Week 5 simulator (Part A, Step 3)

- [x] Gateway pinged and the silent result interpreted correctly (Part B)

- [x] Beacon `ping`, `traceroute`, and `curl` all run and recorded (Part C)

- [x] Beacon banner and TRACE ID recorded (Part C, Step 4)

- [x] `vm-toolkit-live.png` and `beacon-reply.png` captured, cropped, uploaded to `assets/screenshots/week-06/` (Part C, Step 5)

- [x] Ladder Rule rewritten with route evidence + known-good target (Part D)

- [x] All four Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-06/labs/lab-03-the-grid-for-real.md`

---

## GitHub Commit Subsection

1. Open **Week 6 → Lab 03: The Grid, For Real** in the Lab Portal.
2. Fill in the worksheet fields and upload both screenshots to `assets/screenshots/week-06/`.
3. Click **Submit to GitHub** — the Portal commits to `week-06/labs/lab-03-the-grid-for-real.md`.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
