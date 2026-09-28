# Cross-Source Evidence Correlation

## Purpose

This section consolidates the significant findings from the six evidence sources (disk, memory, network, phone – physical, phone – logical and email) and identifies the relationships between them.

A correlation is graded by whether the same identifier, artefact or time relationship is independently present in more than one source. A correlation establishes an environmental or identity relationship; it is not, by itself, evidence of malicious activity.

## Correlation Matrix

| **Finding**                                                                                                     | **Source 1**            | **Source 2**                     | **Relationship**            | **Confidence** |
|-----------------------------------------------------------------------------------------------------------------|-------------------------|----------------------------------|-----------------------------|----------------|
| Computer name M57-JO / owner Jo matches DHCP hostname m57-jo (192.168.1.102)                                    | Disk (registry OS info) | Network (DHCP)                   | Supports                    | **High**       |
| Z: mapped to \\192.168.1.1\m57; 192.168.1.1 is the LAN gateway / DHCP / DNS server                              | Disk                    | Network                          | Supports                    | **High**       |
| Windows XP SP3 host, jo-2009-11-20 naming and Z: path recur in the memory image                                 | Disk                    | Memory                           | Supports                    | **Medium**     |
| 192.168.1.50 (MAC 00:0f:66:ae:e9:8a) shows the same DNS/NTP-type traffic signature across captures              | Network                 | Network (other captures)         | Supports (persistence only) | **High**       |
| Cleartext HTTP login to webmail.m57.biz from 192.168.1.105 (Terry) and 192.168.1.103 (Pat)                      | Network (HTTP POST)     | Network (DHCP, NBNS, HTTP stats) | Supports                    | **High**       |
| Hostnames m57-pat / M57-Terry resemble Address Book contacts Pat / Terry                                        | Network                 | Phone – Logical                  | Contextualises              | **Low**        |
| iPhone OS 4.2.1 (8C148) and iPhone 3G identifiers on the same device                                            | Phone – Physical        | Phone – Logical                  | Supports                    | **High**       |
| +15713083236 appears in both SMS and call-history databases                                                     | Phone – Logical (SMS)   | Phone – Logical (calls)          | Supports                    | **High**       |
| Carved email Pat → Tracy and the "sumtwelve" naming pattern recur in the MacBook email (user tracysumtwelve)    | Phone – Physical        | Email                            | Supports                    | **Medium**     |
| Email of 29 Jun 2012 falls inside the SMS activity window (12 Jun – 5 Jul 2012)                                 | Email                   | Phone – Logical                  | Contextualises              | **Low**        |
| cmd.exe (00:07:03 UTC) → mdd_1.3.exe (00:07:29) → recorded system time (00:07:30)                               | Memory (process list)   | Memory (Info)                    | Supports                    | **High**       |
| 7 Malfind + 12 Suspicious Threads findings vs. the webmail credential event: no connection records to link them | Memory                  | Network                          | Contextualises (no link)    | **Low**        |
| Atera / Kaseya / RDP artefacts show capability; no remote-session evidence in memory or network views           | Disk                    | Memory / Network                 | Contextualises              | **Low**        |

## Significant Correlations

### Correlation 1 — Host identity: disk ↔ network

**Evidence Source A (Disk):** Registry-derived computer name M57-JO, registered owner Jo, organisation M57.biz, Windows XP SP3 (x86). Browser autofill contains j_name=jo and j_email=jo@m57.biz.

**Evidence Source B (Network):** DHCP requests in net-2009-11-15-09_24.dmp identify hostname m57-jo at 192.168.1.102.

**Relationship:** The same host identifier is recovered independently from the registry (disk) and from DHCP options (packet capture).

**Interpretation:** The imaged computer corresponds to the LAN host 192.168.1.102 on the network. This is a host-level link only: the capture (15–16 Nov 2009) predates the disk and memory acquisition (20–21 Nov 2009), so it does not show that the same IP was in use on the day of imaging, and it says nothing about what the user did.

### Correlation 2 — Mapped share and gateway: disk ↔ network

**Evidence Source A (Disk):** Drive Z: is mapped to \\192.168.1.1\m57. The memory image, per the integrated report, also references the Z: path.

**Evidence Source B (Network):** 192.168.1.1 is the gateway, DHCP and DNS server and one of the highest-volume endpoints in the capture.

**Relationship:** The host's configured network share points at the same infrastructure address that dominates the traffic.

**Interpretation:** This is a strong infrastructure correlation that explains the traffic profile of 192.168.1.1. It does not show that the share was used at any specific time, and it is not evidence of unauthorised access.

### Correlation 3 — The confirmed security event and the hosts involved

**Evidence Source A (Network – HTTP):** HTTP POST requests to redirect.php on webmail.m57.biz (208.97.187.139) from 192.168.1.105 (M57-Terry, two logins) and 192.168.1.103 (m57-pat, one login). The login_username and secretkey fields are readable in an application/x-www-form-urlencoded payload.

**Evidence Source B (Network – NBNS/DHCP/HTTP statistics; Phone – Logical):** NBNS queries from 192.168.1.105 for incremental webmail names, HTTP host statistics listing webmail.m57.biz, and DHCP hostnames identifying both hosts. The phone Address Book contains contacts named Pat and Terry.

**Relationship:** The network views reinforce one another (high confidence). The phone contacts only contextualise the hostnames (low confidence): matching first names do not prove the same people.

**Interpretation:** Plaintext credential exposure over unencrypted HTTP is the one confirmed security event. Any observer with access to the LAN path could have read the credentials, but no evidence shows interception, reuse or mailbox compromise. Neither the disk image nor the memory image comes from the Terry or Pat hosts, so they cannot corroborate these logins.

### Correlation 4 — Same device: phone physical ↔ phone logical

**Evidence Source A (Phone – Physical):** SystemVersion.plist reports iPhone OS 4.2.1, build 8C148; 49 EXIF-bearing images carry iPhone 3G identifiers (tracy-phone-2012-07-05.E01).

**Evidence Source B (Phone – Logical):** AppleSupport general.log reports iPhone OS 4.2.1 (8C148), model iPhone1,2 (tracy-phone-2012-07-05.tar).

**Relationship:** Identical OS version, build and device model, plus matching evidence naming, indicate two acquisitions of the same handset.

**Interpretation:** Logical content (SMS, calls, contacts) and physical content (carved email, cookies, EXIF) can be read together as one device profile. This strengthens identity and timeline context but does not by itself indicate malicious activity.

### Correlation 5 — Identity cluster: phone ↔ email

**Evidence Source A (Phone – Physical / Logical):** A message carved from unallocated space (From: Pat TeeSumTwelve \<patsumtwelve@gmail.com\>, To: TracySumtwelve@gmail.com); Address Book entries for Tracy and Pat.

**Evidence Source B (Email):** Sender root@Tracys-MacBook-Air.local, LogKext user account tracysumtwelve, recipient joe.sum.twelve@gmail.com, dated 29 Jun 2012 11:00 -0400. The Message-ID timestamp (15:00:00 UTC) agrees with the Date header.

**Relationship:** A shared "sumtwelve" naming pattern and repeated references to Tracy appear across three sources, although the individual addresses are different.

**Interpretation:** This is a plausible identity cluster around Tracy's devices and accounts in mid-2012, with the email date sitting inside the phone's SMS activity window. It is a naming and timing correlation only. It has no event-level link to the 2009 webmail logins and shows no malicious action.

### Correlation 6 — Persistent unidentified host 192.168.1.50

**Evidence Source A (Network – this capture):** 192.168.1.50 (MAC 00:0f:66:ae:e9:8a) repeatedly queries 4.2.2.3, 4.2.2.4 and 192.168.1.1, including time/NTP-related hostnames.

**Evidence Source B (Network – other captures):** The same IP, MAC and traffic signature recur across three captures, per the integrated report.

**Relationship:** Persistence of the device and its behaviour is directly confirmed.

**Interpretation:** This is a stable, consistently behaving LAN device. The time-related queries are consistent with an automated device, but its identity and purpose are unresolved and nothing here supports treating it as malicious or as the credential observer.

### Correlation 7 — Memory anomalies against the other sources (correlation not established)

**Evidence Source A (Memory):** 7 Malfind-linked and 12 Suspicious Threads findings (non-file-backed VAD regions and/or unexpected PAGE_READWRITE protection) involving csrss.exe (PID 916), lsass.exe (PID 996), avgwdsvc.exe (PID 1684) and explorer.exe (PID 3332). hkemd.exe (PID 3724, C:\WINDOWS\system32\hkemd.exe) was created at 20:00:26 UTC, 36 seconds after explorer.exe (19:59:50 UTC).

**Evidence Source B (Network / Disk):** The packet capture starts on 15 Nov 2009, about five days before the memory image. The memory Network Scan and Network Status exports contain no populated connection records. The disk holds Atera, Kaseya VSA and RDP artefacts but no evidence of a remote session.

**Relationship:** No event-level link exists between the memory anomalies and the network event, the remote-management artefacts or any other source.

**Interpretation:** The memory findings stand as an independent lead. The current hkemd.exe process began after the capture window, although an earlier instance cannot be excluded. The flagged processes are core Windows or security processes, and security software such as the AVG service is one possible benign source of such heuristic hits; this has not been tested. The defensible statement is "suspicious memory anomaly", not "confirmed malware".

### Correlation 8 — Memory acquisition sequence

**Evidence Source A (Memory – Process List):** cmd.exe (PID 3228) created at 00:07:03 UTC, followed by mdd_1.3.exe (PID 2508) at 00:07:29 UTC; the command line shows mdd_1.3.exe writing a RAM image.

**Evidence Source B (Memory – Info):** Recorded system time 2009-11-21 00:07:30 UTC.

**Relationship:** The two process start times lead into the recorded system time within about a minute.

**Interpretation:** This supports reading cmd.exe and mdd_1.3.exe as the acquisition activity that produced the memory image rather than as attacker tooling.

## Contradictions / Inconsistencies

- **Different time bases.** Autopsy displays disk and EXIF times in IST (Asia/Calcutta, the examination time zone), memory is in UTC, and the email uses EDT (-0400). Normalised examples: the USB event 2009-11-20 06:37:33 IST is 01:07:33 UTC; the memory time 2009-11-21 00:07:30 UTC is 2009-11-20 19:07:30 US Eastern standard time, which agrees with the "2009-11-20" in the disk and memory file names; the email time 11:00 EDT is 15:00 UTC. EXIF times carry no zone, so the EXIF conversion (2011-05-29 23:00:53 IST) is uncertain.

- **Sources do not overlap in time.** The packet capture covers about 24 hours from 15 Nov 2009; the memory and disk images date from 20–21 Nov 2009; the phone and email evidence date from 2011–2012 (EXIF 29 May 2011, email 29 Jun 2012, phone image 5 Jul 2012). The evidence therefore cannot be placed on one continuous timeline, and correlations rest on identity and environment rather than shared events.

- **Host mismatch.** The exposed webmail credentials belong to the Terry (192.168.1.105) and Pat (192.168.1.103) hosts, whereas the disk and memory images come from Jo's host (192.168.1.102). The memory image shows Outlook Express (msimn.exe) activity at 22:16:17 UTC on Jo's host, but the capture records HTTP webmail logins from other hosts, so these are different mechanisms.

- **High anomaly counts without corroboration.** Seven Malfind and twelve Suspicious Threads findings contrast with the absence of an identified malicious binary, network records or persistence artefacts, and the flagged processes are mostly core Windows or security components. The indicators are heuristic and unconfirmed.

- **Geographic inconsistency in the phone images.** The EXIF GPS coordinates (18.5887, 73.7807) resolve to western India, whereas the communication artefacts point to the United States (+1 numbers, US-based email accounts, US Eastern time). The images were carved from the System volume (vol4) rather than user media, so their provenance is unresolved.

## Evidence Gaps

- **Credential misuse:** no evidence identifies who, if anyone, captured or reused the exposed credentials; there are no webmail server logs or login-success indicators.

- **Memory to network:** Network Scan and Network Status contain no connection records, so no process can be tied to a remote endpoint.

- **hkemd.exe:** its purpose is unresolved, and the supplied reports do not cross-check it on the disk image (file hash, timestamps, autorun or persistence entries).

- **Flagged memory regions:** the contents of the Malfind and Suspicious Threads regions were not dumped or scanned.

- **192.168.1.50:** device type, owner and function are undetermined.

- **Remote-management tools:** installation and usage times and any remote-session logs for Atera, Kaseya VSA and RDP are not established; these may be legitimate IT tooling.

- **USB and archives:** the 11 USB device records are not tied to any file transfer; the 76 extension mismatches and 12 password-protected archive entries are unresolved.

- **2009 to 2012 link:** nothing connects the phone or MacBook evidence to the M57 network events of 2009.

- **Email:** coralbluetwo@hotmail.com appears only in the LogKext content and is uncorroborated; SPF is Neutral with no DKIM or DMARC result; independent header-analysis output is not reproduced in the artefact table.

- **Integrity:** SHA-256 values for the disk image, memory image, physical phone image and EML file were not supplied in the reports.

## Overall Correlation Assessment

The combined evidence produces strong environmental correlations, chiefly M57-JO/Jo with the DHCP host m57-jo, the Z: mapping with the 192.168.1.1 gateway, and the matching iOS version and device model across the two phone extractions. It also produces plausible identity correlations around Tracy's phone and MacBook. These establish who and what was on the network and on the devices, not whether anything malicious occurred.

The strongest confirmed security event is exposure of the Terry and Pat webmail credentials over unencrypted HTTP, supported by several network views. The memory image is separately suspicious because of repeated heuristic anomalies, but no other source turns those indicators into confirmed malware, remote access or exfiltration.

The evidence does not demonstrate credential interception, account takeover, unauthorised remote access, malware execution or data exfiltration. The supportable conclusion is a confirmed credential-exposure event plus a set of investigative leads, not a fully proven compromise chain.
