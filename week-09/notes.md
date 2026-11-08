# Week 9 Notes - Vault Exchange Digital Trust

**Student Name:** David Wright

**Week:** 9

Use your own words. Short notes and everyday examples are welcome. You do not need to memorize commands.

## From a Key to an Identity

Ivy has two keys with the same label. Why is the label not enough? How can checking a visitor badge help explain the problem?

```text
My explanation: The label is not enough because it doesn't tell which key belongs to which person or what each key can access- each key needs a unique identifier to distinguish it and verify its permissions. Checking a visitor badge can help with this because two visitors might have badges that look identical, but their names, badge numbers, and access permissions could be completely different.
```

## Certificate Fields

A certificate is a digital badge. Explain the name list (SAN), signing office (issuer), start/end dates, public key, signature method, and allowed job (purpose). Which field would you check to see whether the badge covers the right website?

```text
Field and its job: Subject Alternative Name (SAN):  Lists the website names or domains the certificate covers.
Signing Office (Issuer): The Certificate Authority (CA) that issued and signed the certificate.
Start/End Dates: Show when the certificate becomes valid and when it expires.
Public Key:  Used to help establish secure communication and verify digital signatures.
Signature Method: The cryptographic algorithm used by the issuer to sign the certificate and protect its integrity.
Purpose: Defines what the certificate is authorized to do.

I would check the SAN to make sure the badge covers the right website, as the website's domain name must match one of the names listed in the SAN field.
```

## Issuers and Accepted Trust

Who signed the badge? Who chooses whether to accept the top office? Explain why an office signing its own badge is not enough to make your browser trust it.

```text
My explanation: A badge (digital certificate) is signed by a certificate authority (CA), which functions as a trusted signing office. The Root Certificate Authority is the top office, and the browser decides whether to trust it based on its list of trusted root certificates. An office signing its own badge is not enough to make a browser trust it because anyone can create a self-signed certificate and claim to be trustworthy-the browser needs an independent reason to trust that office, such as having its root certificate in the trusted store.
```

## Key CSR and Certificate Roles

The CSR is a badge application. Explain the separate jobs of the service’s private key, application, office’s private key, and finished certificate. Who signs the application? Who signs the finished badge?

```text
My explanation: Service's Private Key: A secret key that belongs to the website or service. It is used to sign the application and must be kept secure.
Application (CSR): Contains the service’s public key and identifying information, such as its domain name, requesting a certificate from a Certificate Authority (CA).
Office’s Private Key: Belongs to the Certificate Authority and is used to sign and issue trusted certificates.
Finished Certificate: The digital badge that contains the service’s public key, identity information, validity dates, and the CA’s digital signature. 

The service signs the application using its own private key, and the CA signs the finished badge using the CA's private key.
```

## TLS and Verification Evidence

Compare looking at a certificate, checking its saved file, and connecting to a running service. TLS sets up a protected connection. What did you observe in each activity?

```text
I looked at:
I checked:
I connected to:
```

## Troubleshooting and Remediation

These words mean finding and fixing a problem. Record an actual message, what it meant, and your next step. Consider a wrong name, expired dates, wrong office, canceled certificate, or service that is not running. Label situations you only discussed; do not claim to have tested them.

```text
Message or situation:
What it means:
What I would check or fix:
Which check I would repeat:
```

## Questions I Still Have

```text
A word or step I want explained again: N/A
```
