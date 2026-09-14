# Week 8 Notes — Practical Cryptography

**Student Name:** David Wright

**Date:** 9/14/2026

## Vocabulary in My Own Words

- Plaintext: the original message or file in its regular, readable form
- Ciphertext: protected output produced by encryption-the message, scrambled
- Encryption: the process that transforms plaintext into ciphertext using a key
- Hash / digest: fixed-length output to compare files to see if any changes have been made
- Public key: one half of a key pair, it encrypts data and is meant to be freely shared
- Private key: the other half of a key pair, it decrypts date and should never be known to anyone but the owner
- Digital signature: a value produced by signing a hash with a private key, and verified with the corresponding public key
- `authorized_keys`: a file on the server that lists public keys allowed to authenticate for a given account

## Command-to-Purpose Map

| Command | What it demonstrated |
| --- | --- |
| `openssl enc`: creating a passphrase
| `sha256sum`: hashing a file
| `ssh-keygen`: generating a key pair
| `openssl dgst': signing an original report
| `ssh ... -o PasswordAuthentication=no': running public-key-only proof

## Safety Rules I Must Remember

1. Never show private key file contents, or your passphrase.
2. Before screenshotting a terminal window, confirm no private key content is visible.
3. Do not display or commit the private key file in GitHub.

## Question for the Instructor

How well do I seem to be mastering the material in this cohort?
