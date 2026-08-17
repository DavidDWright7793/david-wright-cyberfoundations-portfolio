# Week 5 Notes — The Grid: Addresses, Names, Ports, and Diagnostics

**Student Name:** David Wright

**Date Completed:** 8/16/2026

Summarize this week's key concepts in your own words — not copy-pasted definitions.

## Key Concepts This Week

- IP addresses — the dotted-quad number every device on a network needs (`10.20.5.42` on The Grid)
- The subnet mask — the answer to "which addresses are my neighbours?" (`/24` = `255.255.255.0`)
- The default gateway — the door out of your neighbourhood (`10.20.5.1` on The Grid)
- Private vs public addresses — `10.x`, `172.16–31.x`, and `192.168.x` are *inside* addresses
- DNS — the Grid's Directory Board: a name goes in, an IP address comes out
- NXDOMAIN vs a host that resolves but is down — two different failures with two different causes
- DHCP — the Address Office: leases, why addresses change, why a laptop "just works" on a new network
- Ports — the numbered doors on a building: 22 SSH, 53 DNS, 80 HTTP, 443 HTTPS, 3389 RDP, 25 SMTP
- TCP vs UDP — a confirmed conversation vs a shout across the room
- The TCP handshake — SYN → SYN-ACK → ACK (packets 7, 8 and 9 in Lab 03)
- The diagnostic toolkit — `ping` (is it alive?), `traceroute` (where does it stop?), `dig` (what number is behind that name?)
- **THE LADDER RULE** — check yourself → check your gateway → check the target by NAME → check the target by IP → trace the path. *Work outward, one rung at a time, and let the evidence pick the culprit.*

## My Command Table

You learned the same five jobs twice this week — once in bash, once in PowerShell. Fill the pairs in from memory if you can, and check them afterwards. This table is worth keeping.

The bash command and its PowerShell equivalent for each job — show my own address, show my default gateway, test reachability, trace the path, look up a name:

```
Show My Own Address: ip addr (bash) | ipconfig (PowerShell)
Show My Default Gateway: ip route (bash) | ipconfig (PowerShell)
Test Reachability: ping (bash) | Test-Connection (PowerShell)
Trace The Path: traceroute (bash) | tracert (PowerShell)
Look Up A Name: dig (bash) | Resolve-DnsName (PowerShell)
```

## In My Own Words

Your machine has three numbers: an address, a subnet mask, and a default gateway. Explain what each one is for, the way you'd explain it to someone who has never heard those words.

```
An address represents your machine, like the street address for your house. A subnet mask defines which machines are considered part of your local network, similarly to identifying what street your house is on. The default gateway is analogous to the road that leads out of your neighborhood.
```

What does DNS actually do? Include the difference between a name that comes back "Name or service not known" (NXDOMAIN) and a name that resolves perfectly well to a host that never answers.

```
DNS's job can be summarized in four words: name in, number out. It basically tells you what IP address a hostname returns.  A name that returns "Name or service not known" indicates that there is no IP address to send packets to, so there was no communication to the destination. A name that resolves perfectly to an IP address that never answers indicates that DNS successfully translated the hostname into an IP address, but communication with that IP address failed. The first error indicates an inability to find the host, and the second indicates that the host can be located, but it is not responding.
```

An IP address gets your traffic to the right building. What does a port number add to that, and why would a defender care how many doors are open?

```
A port number allows you to access the right "door" in the "building". In other words, the port number allows you to access the right application or service from the IP address. A defender would care about how many doors are open because the more doors that are open, the more openings an attacker has to infiltrate the system-on other words, the attack surface is larger. Opening doors that do not need to be opened to perform a service, and leaving doors open after their service is no longer required, is unnecessarily increasing the attack surface. An analogy is that in your house, you would want to unlock as few doors as possible, only unlock them when you need to use them, and immediately lock them again when you are done using them.
```

Write out THE LADDER RULE — all five rungs, in order — and say why running them in that order matters more than running them fast.

```
The Ladder Rule requires you to work outward, one rung at a time, starting with your own machine. Here are the steps (rungs) of the Ladder Rule in order:

1. Check yourself (ip addr)
2. Check your gateway (ping)
3. Check the target by name (ping)
4. Check the target by IP address (ping)
5. Trace the path (traceroute)

Running them in that order allows you to start by eliminating issues your own workspace, and then eliminate other potential causes, one at a time, working out one step at a time.
```

What is DHCP, and why does your laptop get an address automatically on a network it has never joined before, while a server like `grid-dns` keeps the same address permanently?

```
DHCP is analogous to an Address Office. It automatically assigns your machine an IP address and gives it the information it needs (subnet mask, default gateway, DNS server) to nativate the network and reach places outside of it. DHCP would automatically give my laptop an address on a network it has never joined before because it would be more convenient for it to give me a lease, so they do not have to manually configure every device that joins the network. DHCP often gives certain servers more predictable/permanent addresses, because other devices and applications often need to be able to find them reliably.
```

---

## Submission Checklist

- [x] I summarized each concept in my own words, not copied definitions

- [x] I completed the bash-to-PowerShell command table

- [x] I answered all five "In My Own Words" prompts

- [x] This file is committed to my portfolio repo at `week-05/notes.md`

---

*CyberVisionaries Institute — Cyber Foundations, Tier I*
