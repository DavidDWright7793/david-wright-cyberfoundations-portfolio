# Week 6 Notes — Cloud Heights: Cloud VMs, SSH, VNets & Layers

**Student Name:** David Wright

**Date Completed:** 9/4/2026

Summarize this week's key concepts in your own words — not copy-pasted definitions. This week moved from the simulated Grid into a real cloud environment, so focus on what you personally observed as well as what each term means.

> **Cloud Heights Security Rule:** Your Bastion shareable link and Cloud Heights password are private access credentials. Never paste either into this file, a screenshot, your GitHub repository, Circle, or a chat message.

## Key Concepts This Week

- **Cloud** — other people's computers, professionally operated and reached over a network
- **Datacenter** — the physical facility where cloud computing equipment lives
- **Region** — a geographic area where a cloud provider operates datacenters
- **Virtual machine (VM)** — a computer created in software; in Cloud Heights, your VM runs on hardware in a real datacenter
- **IaaS / PaaS / SaaS** — different levels of cloud service: rent the room, rent the workshop, or rent the finished service
- **Shared responsibility model** — the cloud provider secures the building and underlying platform; the customer is still responsible for what belongs to them
- **Provisioning** — creating and preparing a resource so it is ready to use
- **Golden image / snapshot** — a known starting point that can be used to create consistent machines
- **Snapshot vs backup** — a snapshot is a point-in-time copy used for recovery or cloning; a backup is a separate recovery copy with a different purpose
- **Azure Bastion** — the guarded front desk that gives you browser-based SSH access without giving your VM a public IP
- **Bastion shareable link** — sensitive access information that must never be committed to GitHub or exposed in screenshots
- **SSH (Secure Shell)** — remote command-line access to another machine
- **SSH client and server** — the client starts the connection; the server listens and answers
- **Port 22** — the standard numbered door used by SSH
- **Host / fingerprint verification** — the verify-before-approve habit when connecting to a host for the first time
- **Authentication** — proving that you are the account you claim to be
- **Remote session / remote shell** — the live command-line session running on another machine
- **Getting TO vs getting INTO a machine** — network reachability and authentication are different problems
- **`hostname`** — asks which machine you are on
- **`whoami`** — asks which account you are using
- **`pwd`** — asks where you are in the filesystem
- **Private IP address** — an address used inside a private network rather than directly on the public internet
- **Virtual network (VNet)** — the private cloud neighborhood where resources communicate
- **Subnet** — a smaller address range inside a VNet; a floor inside the larger building
- **NAT / outbound translation** — lets a privately addressed machine communicate outward without giving the machine its own public IP
- **Network Security Group (NSG)** — the network guard post that controls what traffic is allowed; you take control of these rules in Week 7
- **Known-good reference point** — a target whose expected behavior gives you something reliable to compare against
- **Grid Beacon** — the known-good Cloud Heights host at `10.60.6.4`
- **The silent Azure gateway** — Azure's default gateway may not answer ICMP ping even when the network is healthy
- **OSI model** — the seven-layer vocabulary used to organize network and application behavior
- **TCP/IP model** — the more compact layer model commonly used by practitioners
- **Layers** — a way to separate different jobs in a communication path so troubleshooting can be systematic
- **Encapsulation** — information travelling inside other information, like a letter inside an envelope inside a mailbag
- **The Ladder Rule in the real cloud** — work outward, prove what works, use the route and a known-good target, and never let one silent tool response choose the culprit by itself

## My Cloud Heights Command Table

You used these commands on a real Ubuntu machine this week. Instead of memorizing syntax, write down the **question each command answers** or the job it performs.

| Command | What question does it answer / what does it do? |
| --- | --- |
| `hostname` | Which machine am I currently on? |
| `whoami` | Which account am I currently logged into? |
| `pwd` | Which directory am I currently in? |
| `ip addr` | Which IP address is assigned to the machine I am currently on? |
| `ip route` | Where does this machine send traffic that isn't local to this subnet? |
| `ping` | Checks to see if your desired destination responds |
| `traceroute` | Traces the path from your machine to your desired destination |
| `dig` | Tests a destination by name |
| `curl` | Sees if the desired service responds |
| `ssh` | Gain access to SSH service, then provide credentials upon request for authentication |
| `exit` | ends current SSH session |

## In My Own Words

### 1. Getting TO vs Getting INTO

Explain the difference between getting **TO** a machine and getting **INTO** a machine. Use something you personally observed in Cloud Heights as evidence.

```
Getting TO a machine simply means that you can access it, while getting INTO a machine means that you can actually gain access to it. A good analogy is the difference between being able to get to the door of someone else's house and actually being able to go inside the door. The exercise in Lab 2 for Week 6 illustrated this point-when I entered the 'ssh' command, I was prompted to enter a password. I was able to make it to the proverbial door, but I had to enter a password to actually walk through the door.
```

### 2. The Silent Gateway

Your Azure gateway did not answer `ping`, but your VM was still healthy. Explain how you proved the network was working and what this taught you about interpreting tool output.

```
When an Azure gateway does not answer a ping, it represents only one piece of evidence, not a verdict. I was able to prove that the VM was still healthy by by successfully pinging a known-good target. That proved that the gateway was still forwarding traffic to destinations beyond the subnet, even if it was not responding to pings. Also, many gateways, particularly in Azure, are not configured to respond to pings, so that is normal system behavior and not indicative of a problem.
```

### 3. Private on the Inside, Connected to the Outside

Explain how your Cloud Heights VM can reach the internet even though it has only a private IP address. Then explain how **you** reach the VM from outside its VNet.

```
My Cloud Heights VM can reach the internet even though it only has a private IP address because that is how it is designed (for security purposes). There is no public IP address to aim at. Traffic moves through two deliberately different paths. Inbound, you arrive at a guarded front desk-Azure Bastion-which is the only way in. Outbound, your machine reaches the internet through NAT at the loading dock-the platform swaps your private IP address for a shared public one on the way out.
```

### 4. VNet vs Subnet

Explain the difference between a VNet and a subnet using the Cloud Heights building/floor analogy. Then explain why separating systems into smaller network ranges can help security.

```
A VNet is analogous to a building, which is my own private network in the cloud, and nothing outside of it reaches in unless I deliberately build a path. A subnet is analogous to a floor in the building. A private IP address is analogous to a room number on a floor in the building. A primary benefit to separating systems into smaller network ranges is segmentation-if an attacker gains unauthorized access to the server, he/she likely is only able to infiltrate one part of it and does not automatically have unrestricted access to everything else, so that restricts his/her movement and thus the amount (and scope) of damage that he/she is able to do.
```

### 5. The Ladder Rule Has a Map Now

The Ladder Rule never used the words OSI or TCP/IP. Explain how the layer models give you a map for the same troubleshooting process you have already been using.

```
The layers models give a user a similar map for the troubleshooting process that the OSI or TCP/IP models do because both models emphasize working through each layer one at a time, outward, to test and identify the problem.
```

---

## Submission Checklist

- [x] I summarized the Week 6 concepts in my own words, not copied definitions

- [x] I completed my Cloud Heights command table

- [x] I explained getting TO vs getting INTO a machine

- [x] I documented what the silent Azure gateway taught me

- [x] I explained the Cloud Heights private-network design

- [x] I connected the Ladder Rule to network layers

- [x] I checked that my Bastion shareable URL does not appear anywhere in this file

- [x] I checked that my Cloud Heights password does not appear anywhere in this file

- [x] This file is committed to my portfolio repo at `week-06/notes.md`

---

*CyberVisionaries Institute — Cyber Foundations, Tier I*
