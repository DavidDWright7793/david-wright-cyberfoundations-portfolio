# Week 7 Notes — Cloud Heights: The Guard Post

**Student Name:** David Wright

**Week:** 7

## Firewall and Security Group

```text
A firewall is a security control that examines network traffic and decides whether it is allowed through (ALLOW) or blocked (DENY). A simple flow for this is traffic approaches, the firewall evaluates it, and a decision is made. The decision is either ALLOW or DENY, nothing else.
```

## Rule Anatomy

```text
(priority, direction, source, destination, protocol, port, action)
```

## First Match Wins

```text
In a ledger, every rule is attached to a priority number. The lower the priority number, the sooner the rule will be evaluated by the ledger. Evaluation walks the ledger from the lowest priority number upward and stops at the first rule that matches. Everything below that rule is never reached.
```

## Least Privilege

```text
The principle of least privilege is granting exactly the level of access that is required and nothing more. Basically, it opens the narrowest door that still allows the required traffic. An analogy is if a guest checks into a hotel, the desk clerk gives them a key to access the room they reserved, and no other rooms. Giving them access to all rooms would technically do the job (giving them access to the room they reserved), but it would give them access to all the other rooms as well (creating unnecessary risk).
```

## Testing and Evidence

```text
When testing a security rule, it is good practice to test it twice. You should first test to see if the traffic it allows produces an ALLOW verdict. You should then run a second test to prove that the traffic that not allowed produces a DENY verdict. These two pieces of evidence together are stronger proof than either of them are by themselves.
```

## Troubleshooting and Remediation

```text
If a rule does not produce the results you intended, you should check the priority numbers of the relevant rules. The rule you implemented might have a higher priority number than one that contradicts it and thus may never be evaluated.
```

## Questions I Still Have

```text
I still see the concept of subnets as relatively complex, so I would like to learn more about that.
```
