# Week 8 Reflection — Practical Cryptography

**Student Name:** David Wright

**Date:** 9/14/2026

Answer each question in 3–5 sentences.

1. How are encryption and hashing different?

```text
Encryption and hashing do different jobs. Encryption protects the confidentiality of data by making in undecipherable without the right key. Hashing protects the integrity of data by producing a digest of the data that changes if even one character is changed. Encryption does not guarantee a file has not changed, and hashing does not guarantee that a file cannot be read.
```

2. How are symmetric and asymmetric cryptography different?

```text
In symmetric cryptography, the same key both encrypts and decrypts. In asymmetric cryptography, there are two keys that do two different jobs. The public key encrypts and the private key decrypts-neither does both.
```

3. Why does a private key need stronger protection than a public key?

```text
A private key needs stronger protection than a public key because a private key is meant to only be known to the owner, and to never be shared with anyone else. A public key is meant to be freely available. On the other hand, a private key is meant to be a secret.
```

4. What changed between Week 6 password-based SSH and Week 8 key-based SSH? What stayed the same?

```text
Between the Week 6 password-based SSH and Week 8 key-based SSH, several factors stayed the same. The SSH protocol, analyst account,  and VM destination at 'localhost' all stayed the same, and the server still held what it needed for verification. What changed was the method of authentication-I proved that I had the correct private key rather than enter a password.
```

5. Which Week 8 task felt most connected to a real cybersecurity job, and why?

```text
The task of detecting a change in a file in Lab 2 feels a lot like something a real cybersecurity professional would do in their day-to-day work. The task seemed connected to the cybersecurity principle of protecting and preserving integrity of data, and detecting whether said data has changed is a task directly connected to that pillar of the CIA Triad. Immediately becoming aware of any breaches to the confidentiality, integrity, or availability of data seems to be the bread and butter of the cybersecurity profession itself.
```

6. What question do you have about certificates, identity, or trust before Week 9?

```text
As far as trust goes, I would love to learn more about the concept of Zero Trust. I have heard a lot of talk about it in cybersecurity circles, and it would be fascinating to learn more about how it is implemented. It would also be interesting to learn more about how it compares with earlier cybersecurity frameworks, and why it is considered more secure than the ones it replaced.
```
