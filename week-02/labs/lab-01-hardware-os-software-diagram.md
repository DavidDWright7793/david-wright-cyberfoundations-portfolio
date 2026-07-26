# Week 2 Lab 01 — Cybersecurity Landscape & Digital Infrastructure Overview

**Student Name:** David Wright

**Date Completed:**

**Module:** 1 — Digital Infrastructure & CLI | **Week:** 2  
**Submission Path:** `week-02/labs/lab-01-hardware-os-software-diagram.md`

---

## Overview

In this lab, you build a working mental model of the system you'll be securing throughout this course: the hardware, operating system, and software layers that make up every computer, and where the cybersecurity field fits around them. This lab has two parts. Part A connects this week's material to the CyberFoundations City map. Part B has you build and explain a diagram of how a computer's hardware, OS, and software layers interact.

**No terminal or command line is required this week** — that starts in Week 3.

---

## Lab Environment

| Component | Details |
|---|---|
| Environment | Browser-based Lab Portal (Module 1 orientation) |
| Required Materials | CyberFoundations City map; a diagram tool of your choice (hand-drawn and photographed, or any digital tool) |

**Prerequisite:** Portfolio repo created from the CyberFoundations student template in Week 1. Fill out this worksheet here in the Lab Portal, then hit Submit to commit it directly to your repo at `week-02/labs/lab-01-hardware-os-software-diagram.md`.

---

## Part A — CyberFoundations City & the Cybersecurity Landscape

The CyberFoundations City map is your visual guide to the next 11 weeks. Each district represents a module of this course. This part connects this week's material to the map you were introduced to in Week 1.

### Step 1 — Open the Lab Portal Orientation Module

From your Student Dashboard, open the **Module 1 orientation** module.

### Step 2 — Complete the Orientation Walkthrough

Work through the orientation content. It covers the same hardware/OS/software material as this week's lessons from a different angle — use it to check your understanding, not to replace the lessons.

### Step 3 — Locate This Week's District on the City Map

Open the CyberFoundations City map (introduced in Week 1, Lesson 6). Identify which district corresponds to Module 1 — Digital Infrastructure & CLI.

**District name:** Foundry District

```
Foundry District
```

**Why this district fits this week's topics (1–2 sentences):**

```
The Foundry District fits this week's topics because this week introduced the inner hardware components of a computer, as well as different operating systems. The hardware components of computers, and other electronic and technical equipment, correspond perfectly to a "foundry".
```

---

## Part B — Hardware, OS, and Software Diagram

A computer is a stack of layers: physical hardware at the bottom, an operating system managing that hardware in the middle, and the software you actually use on top. This part has you draw that stack and explain it in your own words.

### Step 1 — Identify the Layers

Before drawing anything, name one example of what lives at each layer.

**Hardware layer — one example component (e.g., CPU, RAM, or storage):** CPU

```
The CPU is the sort of "brain" of a computer, as it keeps everything running and functioning.
```

**Operating system layer — name an OS (e.g., Windows, Linux, or macOS):** Windows

```
Windows is an operating system that is most frequently used by personal users (using PCs) or enterprise businesses. It is also a proprietary operating system. Linux, on the other hand, is often used by dedicated servers and for security functions, and is open-source.
```

**Software layer — one example application (e.g., a web browser or word processor):** Web Browser

```
A web browser is a perfect example of software, as it is a program that lives in the computer and is something that a user directly interacts with.
```

### Step 2 — Sketch Your Diagram

Sketch a simple diagram (hand-drawn and photographed, or built in any digital tool) showing how the hardware, OS, and software layers stack and interact. Arrows or labels showing "what talks to what" matter more than visual polish. If you'd like a free browser-based option instead of hand-drawing, try [draw.io](https://www.drawio.com/) — no account required to get started.

### Step 3 — Upload and Embed Your Diagram

This step happens directly on GitHub, not through this worksheet — there's no upload field here, since screenshots and diagrams are added through GitHub's own upload UI, the same way as every other week.

1. Go to your portfolio repository on GitHub.com and navigate to `assets/screenshots/week-02/`.
2. Click **Add file → Upload files**, then drag in your diagram image (name it something descriptive, like `hardware-os-software-diagram.png` — no spaces, lowercase, no timestamps).
3. Commit the upload.
4. Click on the uploaded image to open it, then click the **Raw** button. Copy the URL from your browser's address bar.
5. After you submit this worksheet, it will be committed to your repo. Go back to GitHub, open the committed file, click the pencil (edit) icon, and paste your raw URL into the embed line below:

```markdown
![Hardware/OS/software diagram](paste your raw image URL here)
```

**My Diagram** (added directly on GitHub after you submit):

### Step 4 — Explain Your Diagram

In your own words — not a copied definition — explain how the three layers interact. Reference your own diagram directly.

**Explanation (minimum 3 sentences):**

```
When the user interacts with a computer, they use applications, which are forms of software. The software applications then send a request to the operating system, which then passes it along to the hardware. The hardware passes the requested information to the operating system, and then the operating system relays it to the software applications in order for the user to receive it.
```

---

## Analysis Questions

Answer each question in your own words. These questions connect what you did in Parts A and B to the bigger picture of this course.

### Analysis Question 1

If the operating system crashed on the computer you diagrammed, which layer(s) would stop working, and which (if any) would keep working? Explain your reasoning.

```
If the operating system on a computer crashed, the software would stop working, but the hardware would continue working. The crash of the operating system would leave no way for the user to communicate with the hardware via software, but the harwre would be mostly unaffected.
```

### Analysis Question 2

Pick one piece of software you use daily. Trace it down through the OS to the hardware it ultimately depends on. What would happen to that software if the hardware layer failed?

```
One piece of software I use daily on my computer (Microsoft laptop) is a word processor (Microsoft Word). Microsoft Word depends on storage, as I always save the work I do in there. If the storage in the hardware layer failed, I would not be able to save my work in Microsoft Word. Without functional storage in hardware, Microsoft Word would not even be able to open.
```

### Analysis Question 3

Explain, in your own words, why a cybersecurity professional needs to understand all three layers — hardware, OS, and software — rather than just the software layer where most visible attacks (like phishing emails) happen.

```
A cybersecurity professional needs to understand all three layers of a computer-hardware, OS, and software-rather than just the software layer because attacks can happen to any of the layers. Even though the software layer is where the most visible attacks happen, if the OS or hardware is attacked, that would render the software unusable. The OS needs to be understood and secured because it is what allows the user to communicate with the hardware via the software. The hardware needs to to be understood because it is what makes the computer operational in the first place, and its failure would make everything else in the computer unusable.
```

---

## Lab Report Questions

Answer each question in complete sentences.

**1. What is the cybersecurity landscape, and why does it matter to someone starting this course?**

```
The cybersecurity landscape is the overall picture of who is attacking data, systems, and people, how they are attacking, and why they are attacking at any given time. The cybersecurity landscape is important for cybersecurity students to understand, as they need to know what they will be protecting, who they will be protecting from, how they will be protecting from these threat actors, and why the threat actors would employ their tactics and how to counter them. All of these things are ever-changing, so it is vital for cybersecurity professionals to engage in continuous educaton to keep up with these ever-evolving threats.
```

**2. Which CyberFoundations City district did you identify in Part A, and how does its theme connect to the hardware/OS/software material in Part B?**

```
The CyberFoundations City district I identified in Part A was the Foundry District. The theme of the Foundry District connects to the hardware/OS/software material in Part B because those three components for the basic mechanical function of a computer, and are thus its backbone. The computer wouldn't run at all without its hardware (the "foundry"), and users would not be able to communicate with the hardware without the software and OS.
```

**3. Of the three layers (hardware, OS, software), which one do you think is hardest to secure, and why?**

```
Of the three layers, I think that software is the hardest to secure, as software can offer a tremendous amount of entry points to an attacker, as software is highly complex. With hardware, there are more concrete limits on how many points of entry a threat actor can exploit. Software also needs to be constantly updated and patched in order to fix bugs and vulnerabilities, and maintain its secure status.
```

---

## Submission Checklist

- [ ] Lab Portal Module 1 orientation completed

- [ ] District identified and explained

- [ ] Hardware, OS, and software layer examples listed

- [ ] Diagram uploaded to `assets/screenshots/week-02/` via GitHub and embedded directly in the committed file

- [ ] Diagram explanation written in your own words (minimum 3 sentences)

- [ ] All three Analysis Questions answered (minimum sentence counts met)

- [ ] All three Lab Report Questions answered in complete sentences

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
