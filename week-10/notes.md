# Week 10 Notes — Security Fundamentals and Risk

**Student Name:** David Wright

**Date:** 10/9/2026

Use your own words and everyday examples. These notes support your thinking; they are not your lab answers. Do not copy clinic scenario answers here — those belong in the Demo Lab.

## 1. Assets and Business Purpose

An asset is something a business depends on. Pick an everyday example (a bakery, a gym, a school).

```text
My everyday business: A timeshare resort
One asset it depends on: Desktop computers at the front desk and the accompanying reservation/guest management application (TSW Production)
Why the business needs that asset: We need the computers at the front desk to do our administrative work at the hotel (checking guests in, taking payments for reservations, entering maintenance requests, sending and checking email, etc.) and we need TSW Production to keep track of guest reservations and in-house guests, check guests in, adjust reservations, take payments, etc.
```

## 2. Confidentiality, Integrity, Availability

Define each goal in your own words, then describe one situation where more than one goal is affected and explain why.

```text
Confidentiality means: Information/data is only visible and accessible to those who are authorized to view and/or access it.
Integrity means: Information/data is complete and accurate, and is not altered, corrupted, or deleted.
Availability means: Information/data is available to parties that are authorized to access it, and is available when they need to access it,
A situation where goals overlap, and why: If the desktop computers at our front desk are hacked, each pillar of the CIA triad (confidentiality, integrity, availability) could potentially be affected. An unauthorized individual could illicitly access those computers and steal credit card numbers from our member records or reservations in order to make unauthorized purchases with the cards (a violation of confidentality). They could alter the information on reservations (or the reservations themselves) to prevent us from properly accommodating the guests (a violation of integrity). They could hack our computers and completely block access to the applications that manage reservations (such as TSW Production), so we do not have the information that we need to perform our job duties (a violation of availability).
```

## 3. Event, Weakness, Consequence and Risk

Use your OWN non-clinic example to separate these four ideas.

```text
My example setting: Timeshare resort
Threat / event (what could happen): The computers at the front desk are hacked, and the reservation/guest management system (TSW Production) is blocked from use by employees.
Vulnerability (the weakness that lets it cause harm): The computers have not been given security updates within a proper timeframe.
Consequence (what goes wrong if it happens): If the computers at the front desk are hacked by a threat actor and TSW Production is disabled, the front desk staff will not be able to perform the necessary tasks that keep the resort's systems running. If TSW Production is blocked from use by employees, they cannot use the system to check guests in or out, make sure guests are sent to the correct room number for their reservation, program keys for the correct room number and length of stay, or take credit card payments for reservations. Hackers can also steal guests' information from the system, such as their credit card numbers (to make unauthorized purchases) and contact information (to send them phishing emails or otherwise scam them).
Risk (how the pieces combine into something to manage): If the computers at the front desk suffer a security breach (they could be hacked, infected with malware, or even just physically accessed by an unauthorized individual), that could result in violations of confidentiality (guest data could be viewed, distributed, and used by unauthorized individuals), integrity (guest data could be incorrectly altered or erased), and availability (resort staff could be blocked from using TSW Production).
```

## 4. Observed, Inferred and Unknown

Evidence you saw is different from a guess. If you did not see a safeguard, it is unknown — not proof it is missing.

```text
Something I observed directly: evidence
Something I inferred from it: risk
Something that is still unknown: uncertainty
How I will label a safeguard I did not see: unknown
```

## 5. Warning Signs and Safe Reporting

Suspicious is not the same as proven.

```text
Warning signs I would look for: A sense of urgency in the email, the email domain is irregular, the email is asking the user to confirm their name and current password on another site.
How I would safely verify without clicking or replying: Call the known, official number of the entity and ask if they truly did send the email.
Who I would report to, and how: I would immediately report a suspicious email to IT/security through the designated reporting mechanism. I woudl also report it to the manager/supervisor of my department.
Why suspicion alone does not prove compromise: Suspicious signs only indicate compromise, not prove it. There could be legitimate reasons for certain anomalies.
```

## 6. Likelihood and Impact

Likelihood and impact are each rated 1–3. The classroom score is Likelihood x Impact. Bands: 1–2 low, 3–4 medium, 6–9 high. These are classroom judgments, not measured probabilities.

```text
What a likelihood of 1, 2 or 3 means to me: A likelihood of 1-3 means that there is a low probability of the event occurring, as there are few vulnerabilities and enough protections in place to stop the event if it does occur.
What an impact of 1, 2 or 3 means to me: An impact of 1-3 means that if the event occurs, it only amounts to a minor inconvenience, as normal operations continue and no sensitive data is affected.
Existing controls vs proposed controls, in my words: An existing control is a safeguard that is already described and operating in the case, and a proposed control is a planned safeguard that is not yet operating in the environment.
Why recording my reason matters more than the number: Recording my reason matters more than the number because a stated reason gives much more context and insight into a risk than a simple numerical rating does.
```

## 7. Controls and Residual Risk

Use a non-clinic example.

```text
A specific control: At the timeshare resort I work at, we usually lock our desktop computer screens when we step away from the computers.
How it helps: If an unauthorized individual gains access to the computers at the front desk, it is harder for them to gain access to our systems. It is also harder for a disgruntled coworker to jump into our account on the computer.
Risk remaining afterwards: Locking the computer screens when stepping away from the computer does not prevent threat actors from physically accessing the computers themselves.
```

## 8. Talking to a Manager

```text
How I would explain a risk in plain language to a non-technical manager: I would explain a risk as an event that could adversely affect the organization, and then tell them the factors that make it likely or possible, and then the impct and consequences if it does occur.
```

## 9. Questions and Terms to Revisit

```text
Terms I want to review: N/A
Questions for my instructor: Do I seem to have a solid command of risk management?
```
