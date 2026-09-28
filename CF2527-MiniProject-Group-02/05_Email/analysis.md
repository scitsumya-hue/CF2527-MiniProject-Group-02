# Email Investigation — Detailed Forensic Analysis

## 1. Evidence Information

| Field | Details |
|---|---|
| Evidence Category | Email / EML |
| Evidence File | `logfile-2012-06-29-1100.eml` |
| Case | `Email_Investigation` |
| Case Number | `Not provided` |
| Analyst | `Not provided` |
| Analysis Method | Manual email-header and body analysis |
| Evidence SHA-256 | `43b6e813d69b09b6c8dc169e1ae88453b40d64fb396959aa7041c24084fc5fff` |

## Evidence Integrity Note

The supplied EML file was hashed using SHA-256:

`43b6e813d69b09b6c8dc169e1ae88453b40d64fb396959aa7041c24084fc5fff`

This value identifies the supplied EML evidence file. It is not a hash embedded in the email itself.

---

## 2. Objective

The objective is to examine the supplied email evidence and identify relevant artefacts including:

1. Sender and recipient
2. Sending IP
3. Originating server/host
4. Mail servers and delivery path
5. SPF, DKIM and DMARC results
6. Relevant domains and URLs
7. IP addresses and timestamps
8. Message identifiers
9. Suspicious or unusual headers
10. Potential indicators of compromise
11. Evidence supporting or contradicting phishing, spoofing or suspicious-mail hypotheses
12. Correlation between the email headers and the logged content

The analysis separates direct observations from interpretation.

---

# 3. Methodology

The supplied EML was examined as a raw email message.

The analysis focused on:

- `From`
- `To`
- `Delivered-To`
- `Return-Path`
- `Received`
- `Received-SPF`
- `Authentication-Results`
- `Subject`
- `Date`
- `Message-ID`
- Presence or absence of `DKIM-Signature`
- Presence or absence of DMARC results
- Message body and LogKext artefacts
- Email addresses, domains and IP addresses contained in the message

MxToolbox is required by the assignment for independent email-header analysis. No MxToolbox result was supplied with the evidence package, so this report does not fabricate an MxToolbox result. The manual analysis should be compared with the actual MxToolbox output after it is captured.

---

# 4. Analysis of Findings

## 4.1 Sender and Recipient

### Observation

The message contains:

- **From:** `root@Tracys-MacBook-Air.local`
- **To:** `joe.sum.twelve@gmail.com`
- **Delivered-To:** `joe.sum.twelve@gmail.com`
- **Return-Path:** `root@tracys-macbook-air.local`

### Interpretation

The visible sender and Return-Path both identify the local `.local` host. The recipient is the Gmail account `joe.sum.twelve@gmail.com`.

### Finding

The email evidence establishes `root@Tracys-MacBook-Air.local` as the address in the From header and `joe.sum.twelve@gmail.com` as the intended/delivered recipient.

---

## 4.2 Date and Time

### Observation

The Date header is:

`Fri, 29 Jun 2012 11:00:00 -0400 (EDT)`

The local Postfix Received entry records:

`Fri, 29 Jun 2012 11:00:00 -0400 (EDT)`

Google's receipt entries record approximately:

`Fri, 29 Jun 2012 08:00:02–08:00:04 -0700 (PDT)`

### Interpretation

The displayed times use different timezone offsets, but represent the same general delivery event. The email was generated and delivered on 29 June 2012.

### Finding

The message timestamp is internally consistent with the local Postfix generation and subsequent Google receipt records.

---

## 4.3 Sending IP and Originating Host

### Observation

The relevant Received entry states that the message was received:

`from Tracys-MacBook-Air.local ([2600:1003:b02a:3724:c15:34bf:4761:9c36]) by mx.google.com`

### Interpretation

The apparent external sending IP is `2600:1003:b02a:3724:c15:34bf:4761:9c36`. The hostname associated with that hop is `Tracys-MacBook-Air.local`.

### Finding

The supplied header evidence identifies `2600:1003:b02a:3724:c15:34bf:4761:9c36` as the apparent sending IP and `Tracys-MacBook-Air.local` as the originating host in the external Received hop.

---

## 4.4 Local Mail Submission

### Observation

The EML contains:

`Received: by Tracys-MacBook-Air.local (Postfix, from userid 0)`

with queue/message identifier:

`3AAD564693`

### Interpretation

The message was submitted locally through Postfix and the header identifies `userid 0`, which corresponds to the root/superuser account on a Unix-like system.

### Finding

The email was locally generated/submitted through Postfix under userid 0. This is strong evidence of local message generation, but it does not identify the human operator.

---

## 4.5 Mail Delivery Path

### Observation

The visible Received chain contains:

1. `Tracys-MacBook-Air.local` → `mx.google.com`
2. Google internal server `10.236.191.138`
3. Google internal server `10.114.63.177`

### Interpretation

The message was generated locally and then accepted by Google's mail infrastructure before delivery to the recipient mailbox.

### Finding

The available headers provide a delivery path from the local originating host to Google infrastructure and finally to the Gmail recipient.

---

## 4.6 SPF

### Observation

The header contains:

`Received-SPF: neutral`

The Authentication-Results header also reports:

`spf=neutral`

### Interpretation

Google's result states that the sending IP was neither permitted nor denied by the best-guess SPF record for the sender domain `tracys-macbook-air.local`.

### Finding

SPF is **Neutral**. It does not positively authenticate the sender and does not, by itself, prove spoofing or malicious activity.

---

## 4.7 DKIM

### Observation

No `DKIM-Signature` header is present in the supplied EML. No DKIM authentication result is present in the Authentication-Results header.

### Finding

**DKIM: Not present / not verifiable from the supplied EML.**

It should not be described as a DKIM failure because the supplied evidence does not establish a failed DKIM verification.

---

## 4.8 DMARC

### Observation

No DMARC authentication result is present in the supplied EML.

### Finding

**DMARC: No result present in supplied headers.**

The evidence therefore does not establish a DMARC pass or failure.

---

## 4.9 Message-ID

### Observation

The Message-ID is:

`<20120629150000.3AAD564693@Tracys-MacBook-Air.local>`

### Interpretation

The Message-ID uses the local hostname `Tracys-MacBook-Air.local`.

### Finding

The Message-ID is consistent with local message generation on the originating host.

---

## 4.10 Email Body / LogKext Evidence

### Observation

The message body identifies:

- `LogKext Daemon created new logfile : Thu Jun 28 16:09:50 2012`
- `LogKext Daemon starting up : Fri Jun 29 09:04:12 2012`
- `User 'tracysumtwelve' has logged in : Fri Jun 29 09:14:10 2012`
- `LogKext Daemon starting up : Fri Jun 29 10:33:05 2012`
- `User 'tracysumtwelve' has logged in : Fri Jun 29 10:33:25 2012`

The body also contains:

`coralbluetwo@hotmail.com`

and fragments of captured conversational/textual material.

### Interpretation

The body is consistent with a logfile containing system/user activity rather than a conventional manually composed email.

### Finding

The email contains evidence of local logging activity and transmission of the resulting log information.

---

## 4.11 Body Content Integrity / Truncation

### Observation

The body contains `<del>` and `<tab>` markers and several incomplete words or phrases.

### Interpretation

These markers appear to represent transformed, deleted or control-character content in the supplied evidence.

### Finding

The exact missing content cannot be reliably reconstructed. The analysis therefore records only the text that is directly observable.

---

## 4.12 Domains and Email Addresses

### Observation

Relevant values include:

| Value | Context |
|---|---|
| `Tracys-MacBook-Air.local` | Originating host / Message-ID |
| `gmail.com` | Recipient service |
| `hotmail.com` | Domain of an address captured in the log |
| `coralbluetwo@hotmail.com` | Address present in body |
| `joe.sum.twelve@gmail.com` | Recipient |

### Finding

The Hotmail address is contained within the logged content and is **not** the sender of the email under investigation.

---

## 4.13 URLs

### Observation

No complete HTTP/HTTPS URL was identified in the supplied EML.

### Finding

**URLs: None identified.**

An email domain or email address should not be treated as a URL.

---

# 5. Indicators of Compromise

| IOC Type | Value | Significance |
|---|---|---|
| IP | `2600:1003:b02a:3724:c15:34bf:4761:9c36` | Apparent external sending address |
| Host | `Tracys-MacBook-Air.local` | Originating system |
| Email Address | `coralbluetwo@hotmail.com` | Email address found inside logged content |
| Email Address | `joe.sum.twelve@gmail.com` | Recipient |
| URL | None identified | No URL present in supplied evidence |
| Hash | `43b6e813d69b09b6c8dc169e1ae88453b40d64fb396959aa7041c24084fc5fff` | SHA-256 of supplied EML evidence |

These are **candidate investigation indicators**. Their presence does not by itself establish maliciousness.

---

# 6. Phishing / Spoofing / Suspicious-Mail Assessment

### Evidence supporting a suspicious-mail hypothesis

- SPF is Neutral rather than a positive authentication result.
- No DKIM signature is present.
- No DMARC result is present.
- The sender uses a `.local` hostname.
- The message contains system/user logging information.

### Evidence against a conventional phishing interpretation

- No URL was identified.
- The message does not contain a conventional credential-harvesting or payment lure in the supplied content.
- The message appears to have been generated locally through Postfix.
- The body is primarily logfile content rather than a conventional phishing message.

### Finding

The supplied evidence is more consistent with an email used to transmit locally collected logging information than with a conventional phishing email. The EML alone does not establish whether the activity was authorized or malicious.

---

# 7. Cross-Artefact Correlation

## 7.1 Header-to-Body Correlation

The header identifies `Tracys-MacBook-Air.local` as the originating host. The body simultaneously contains LogKext daemon records and user login events.

This provides a direct correlation between the email transport metadata and the logged system activity contained within the message.

## 7.2 Local Generation-to-External Delivery

The Postfix entry records local submission from userid 0. The subsequent Received entry shows delivery from the local host to `mx.google.com`.

This provides a coherent sequence:

**Local Postfix generation → Tracys-MacBook-Air.local → sending IP → Google mail infrastructure → Gmail recipient**

## 7.3 Log Collection-to-Email Transmission

The body contains LogKext records and captured content, while the email itself is addressed to an external Gmail mailbox.

This supports the interpretation that the collected log information was transmitted through email.

---

# 8. Timeline of Selected Events

| Date/Time | Evidence | Interpretation |
|---|---|---|
| 2012-06-28 16:09:50 | LogKext created new logfile | Logging activity begins |
| 2012-06-29 09:04:12 | LogKext daemon started | Logging process activity |
| 2012-06-29 09:14:10 | User `tracysumtwelve` logged in | Recorded user login |
| 2012-06-29 10:33:05 | LogKext daemon started | Logging process activity |
| 2012-06-29 10:33:25 | User `tracysumtwelve` logged in | Recorded user login |
| 2012-06-29 11:00:00 EDT | Postfix generated message | Local email generation |
| 2012-06-29 08:00:02–08:00:04 PDT | Google received message | External mail delivery |

The timestamps are reported as recorded by the respective artefacts. They should not automatically be treated as proof of direct human action.

---

# 9. Significance Assessment

| Finding | Significance | Assessment |
|---|---|---|
| Local Postfix generation | Message origin | Significant |
| `userid 0` | Local privileged submission | Significant |
| Sending IPv6 address | Network indicator | Significant |
| SPF Neutral | Authentication | Requires interpretation |
| No DKIM | Authentication | No positive DKIM authentication |
| No DMARC result | Authentication | No DMARC result available |
| LogKext records | System/user logging | Significant |
| User login records | User activity | Significant |
| `coralbluetwo@hotmail.com` | Captured email address | Investigation lead |
| No URLs | Phishing analysis | No URL-based lure identified |

---

# 10. Limitations

1. The analysis is based on the supplied EML file.
2. No MxToolbox output was supplied or captured for this report.
3. No DKIM signature is present in the supplied EML.
4. No DMARC result is present in the supplied EML.
5. SPF is Neutral and therefore does not positively authenticate the sender.
6. The message body contains `<del>` and `<tab>` markers and truncated content.
7. The EML does not establish the identity or intent of the person who configured the logging/transmission.
8. The apparent sending IP is a header-derived network indicator and should be independently validated with the original forensic context.
9. The presence of logging data does not by itself prove unauthorized surveillance, compromise or data exfiltration.

---

# 11. Final Conclusion

The supplied EML provides evidence of a locally generated message sent from `root@Tracys-MacBook-Air.local` to `joe.sum.twelve@gmail.com`. The header chain identifies `Tracys-MacBook-Air.local` and `2600:1003:b02a:3724:c15:34bf:4761:9c36` as the originating host/IP combination and shows local Postfix submission followed by delivery through Google infrastructure.

Authentication evidence is limited: SPF is Neutral, while DKIM and DMARC results are absent. The body contains LogKext daemon activity, user login records and captured textual material including `coralbluetwo@hotmail.com`.

The combined evidence supports the conclusion that the email was used to transmit locally collected logging information. It does not independently establish malicious intent, unauthorized access or the identity of the person responsible. Those questions require additional host, network and account evidence.
