# Email Investigation — Summary

## 1. Case and Evidence Information

| Field | Details |
|---|---|
| Case Name | `Email_Investigation` |
| Case Number | `Not provided` |
| Evidence File | `logfile-2012-06-29-1100.eml` |
| Evidence Type | Email / EML |
| Data Sources | 1 |
| Examiner / Analyst | `Not provided` |
| Forensic Tool | Manual email-header analysis; MxToolbox analysis to be documented separately |
| Evidence SHA-256 | `43b6e813d69b09b6c8dc169e1ae88453b40d64fb396959aa7041c24084fc5fff` |
| Email Date | `29 Jun 2012, 11:00:00 -0400 (EDT)` |

> **Integrity note:** The SHA-256 value above was calculated from the supplied EML file. The original EML is the evidence source used for the manual header analysis.

---

## 2. Executive Summary

The supplied evidence is an EML file with the subject **Logfile**. The message was addressed from `root@Tracys-MacBook-Air.local` to `joe.sum.twelve@gmail.com` and contains mail headers showing local generation on `Tracys-MacBook-Air.local` using Postfix, followed by delivery through Google's mail infrastructure.

The apparent sending IP is `2600:1003:b02a:3724:c15:34bf:4761:9c36`. The supplied authentication results show **SPF: neutral**. No DKIM signature or DKIM result and no DMARC result are present in the supplied headers.

The message body contains **LogKext Daemon** logging artefacts, user login events for `tracysumtwelve`, and captured text containing the email address `coralbluetwo@hotmail.com`. The evidence therefore supports an interpretation that the message was used to transmit locally collected logging information rather than functioning as a conventional personal email.

The supplied EML alone does not establish who configured the logging process, the intent behind the collection, or whether the activity was authorized.

---

## 3. Key Artefact Statistics

- **Sender:** `root@Tracys-MacBook-Air.local`
- **Recipient:** `joe.sum.twelve@gmail.com`
- **Sending IP:** `2600:1003:b02a:3724:c15:34bf:4761:9c36`
- **Originating host:** `Tracys-MacBook-Air.local`
- **Mail server:** `mx.google.com`
- **SPF:** `Neutral`
- **DKIM:** `Not present in supplied headers`
- **DMARC:** `Not present in supplied headers`
- **Message-ID:** `<20120629150000.3AAD564693@Tracys-MacBook-Air.local>`
- **Email address found in logged content:** `coralbluetwo@hotmail.com`
- **User account recorded in log:** `tracysumtwelve`
- **URLs identified:** None
- **EML SHA-256:** `43b6e813d69b09b6c8dc169e1ae88453b40d64fb396959aa7041c24084fc5fff`

---

## 4. Major Findings

### 4.1 Sender / Recipient

The `From` header identifies `root@Tracys-MacBook-Air.local` and the `To` header identifies `joe.sum.twelve@gmail.com`. The `Delivered-To` header also identifies `joe.sum.twelve@gmail.com`.

### 4.2 Originating Host and Sending IP

The external `Received` header records the message as being received from `Tracys-MacBook-Air.local` using IPv6 address `2600:1003:b02a:3724:c15:34bf:4761:9c36` and delivered to `mx.google.com`.

The message was also locally submitted through **Postfix** using `from userid 0`. This is consistent with local generation under the root/superuser account, although it does not independently establish who was operating the system.

### 4.3 Authentication

**SPF:** Neutral. The Google authentication result states that the sending IP was neither permitted nor denied by the best-guess SPF record for the `.local` sender domain.

**DKIM:** No `DKIM-Signature` or DKIM authentication result is present in the supplied EML.

**DMARC:** No DMARC authentication result is present in the supplied EML.

### 4.4 Message Identification

The Message-ID is:

`<20120629150000.3AAD564693@Tracys-MacBook-Air.local>`

The Message-ID uses `Tracys-MacBook-Air.local`, which is consistent with the originating host shown in the Received chain.

### 4.5 LogKext Evidence

The body contains entries identifying the **LogKext Daemon**, including:

- Logfile creation on 28 June 2012 at 16:09:50
- LogKext startup on 29 June 2012 at 09:04:12
- User `tracysumtwelve` login at 09:14:10
- LogKext startup at 10:33:05
- User `tracysumtwelve` login at 10:33:25

The body also contains captured text and the email address `coralbluetwo@hotmail.com`. Parts of the captured content contain `<del>` markers and appear truncated or transformed, so missing text should not be reconstructed as fact.

### 4.6 URLs and Domains

No URL was identified in the supplied EML.

Relevant domains/hosts are:

| Domain / Host | Significance |
|---|---|
| `Tracys-MacBook-Air.local` | Originating local host and Message-ID host |
| `gmail.com` | Recipient mail service |
| `hotmail.com` | Domain of an email address found within the logged content |

---

## 5. Potential Indicators of Compromise

| IOC Type | Value | Significance |
|---|---|---|
| IP | `2600:1003:b02a:3724:c15:34bf:4761:9c36` | Apparent external IPv6 address in the Received chain |
| Host / Domain | `Tracys-MacBook-Air.local` | Originating host |
| Email Address | `coralbluetwo@hotmail.com` | Address captured in the logged content |
| Email Address | `joe.sum.twelve@gmail.com` | Recipient of the evidence email |
| URL | None identified | No URL found in supplied EML |
| File / Hash | `43b6e813d69b09b6c8dc169e1ae88453b40d64fb396959aa7041c24084fc5fff` | SHA-256 of supplied EML evidence file |

---

## 6. Interpretation

The header evidence indicates that the message was generated locally on `Tracys-MacBook-Air.local` using Postfix and subsequently delivered to a Gmail mailbox. SPF returned Neutral, while DKIM and DMARC authentication results are absent.

The body is more significant than the authentication results alone. It contains LogKext daemon output and recorded user login events, together with captured textual material. This supports the interpretation that the email transmitted locally collected logging information.

The evidence does not, by itself, establish whether the logging and transmission were authorized or malicious.

---

## 7. Correlation

The strongest correlation is between:

1. The local originating host in the Received header.
2. The Postfix local submission entry.
3. The LogKext logfile content in the message body.
4. The user login records for `tracysumtwelve`.
5. The external recipient `joe.sum.twelve@gmail.com`.

These artefacts are consistent with a workflow in which locally collected logging information was packaged into an email and transmitted externally.

Further host, network and account evidence would be required to establish configuration, authorization and intent.

---

## 8. Limitations

1. The analysis is based on the supplied EML file.
2. No DKIM signature is present in the supplied headers.
3. No DMARC result is present in the supplied headers.
4. SPF is Neutral and therefore does not positively authenticate the sender.
5. The body contains `<del>` markers and truncated content, so missing text cannot reliably be reconstructed.
6. The EML alone does not establish the identity or intent of the person responsible for the logging/transmission.
7. MxToolbox output has not been inserted into this document because no MxToolbox result was supplied or captured. The manual header findings should be retained alongside the actual MxToolbox output once obtained.

---

## 9. Overall Conclusion

The supplied EML establishes that a message titled **Logfile** was sent from `root@Tracys-MacBook-Air.local` to `joe.sum.twelve@gmail.com`. The message contains an originating-host and sending-IP trail, SPF Neutral authentication, and no DKIM or DMARC result.

The message body contains LogKext daemon activity, user login records and captured textual content, including `coralbluetwo@hotmail.com`. Taken together, the evidence supports the conclusion that the email transmitted locally collected logging information.

The evidence does not independently establish malicious intent, unauthorized access or the identity of the person responsible. Those conclusions would require correlation with additional host, network and account evidence.
