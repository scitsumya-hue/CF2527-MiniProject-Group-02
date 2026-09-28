# Final Investigation Findings

## 1. Investigation Overview

This investigation examined six evidence sources: a disk image, a memory image, a physical and a logical phone extraction, an email (EML), and a network packet capture (PCAP). The objective was to identify security-relevant events, correlate artefacts across sources, and state which conclusions the evidence supports and which it does not.

The strongest confirmed security event is the exposure of webmail credentials over unencrypted HTTP. The memory image contains suspicious anomalies. The disk, phone and email evidence provide identity, environment and timeline context. No source independently establishes an attacker, malware execution, unauthorised remote access or data exfiltration.

## 2. Evidence Sources

| Source | Evidence item | Tool(s) | Integrity reference |
|---|---|---|---|
| Disk image | `jo-2009-11-20-oldComputer.E01` (13,020,069,888 bytes; Windows XP SP3 x86; host M57-JO) | Autopsy 4.23.1 | SHA-256 `c141e380cb8e642dc5a905f253577dcf3dc205ebe97383ac00f2a18c6e3031cf` |
| Memory image | `67210fe41fe5-jo-2009-11-20.mddramimage` (Windows XP SP3, 32-bit) | VolViewer | SHA-256 `3871F3AF1A93C05DB93080EA336D8AD2E8C9F59AFC5B3D8BAE99BEE2D45A5805` |
| Phone – Physical | `tracy-phone-2012-07-05.E01` (iPhone OS 4.2.1, build 8C148) | Autopsy 4.23.1 | SHA-256 `7410eb756ed1af9e12d8d8873f9faa164076214a62a042d1b93b3d935e7333b7` |
| Phone – Logical | `tracy-phone-2012-07-05.tar`, extracted to `D:\DF2` | DB Browser for SQLite, Windows file examination | SHA-256 `aa8ac5304f5f12cf1eecb8462bd7aac5225f05ac42115bfebf5ad56befe86005` |
| Email | Supplied EML (subject "Logfile", 29 Jun 2012) | Manual header and body analysis; MxToolbox planned | SHA-256 `43b6e813d69b09b6c8dc169e1ae88453b40d64fb396959aa7041c24084fc5fff` |
| Network / PCAP | `net-2009-11-15-09_24.dmp` (33,773 packets, about 24 hours) | Wireshark | SHA-256 `f35e39a7d8533c07341ce490b9db00a93b5815e9defae87919d85425c9173a92`; MD5 `fca2c71fbee313bc60cb79bee3e19451` |

## 3. Major Findings

### Disk

- Host identified as **M57-JO**, Windows XP SP3 x86, registered owner **Jo**, organisation M57.biz.
- Browser artefacts: 3,733 web-history records, 39 searches, 310 cookies, 10 autofill records. Autofill includes `j_name=jo` and `j_email=jo@m57.biz`.
- Drive **Z:** is mapped to `\\192.168.1.1\m57`.
- Atera, Kaseya VSA and Microsoft RDP artefacts were found under Remote Monitoring Management programs.
- 11 USB device records were recovered, including a Logitech mouse, a Dell keyboard and mouse, Alcor Micro and Imation flash drives, and a LaCie rugged mobile hard drive.
- 76 extension-mismatch records and 12 password-protected archive entries were identified.
- **Assessment:** these are host, user and environment context and investigative leads. They do not show unauthorised access, file transfer or tampering.

### Memory

- Windows XP SP3, 32-bit, one processor. Recorded system time 2009-11-21 00:07:30 UTC. 38 timestamped process events.
- Malfind returned **7** linked findings and Suspicious Threads returned **12**. Both involve non-file-backed VAD regions and/or unexpected `PAGE_READWRITE` protection. Associated processes include `csrss.exe` (916), `lsass.exe` (996), `avgwdsvc.exe` (1684) and `explorer.exe` (3332).
- `hkemd.exe` (PID 3724, `C:\WINDOWS\system32\hkemd.exe`, started 2009-11-20 20:00:26) requires contextual identification.
- `cmd.exe` (PID 3228) and `mdd_1.3.exe` (PID 2508, 2009-11-21 00:07:29) are consistent with the RAM acquisition itself.
- Network Scan and Network Status exports contain no populated connection records.
- **Assessment:** a suspicious memory anomaly. Malfind and Suspicious Threads are heuristic indicators and do not prove malware or injection.

### Phone – Physical

- Volumes identified: vol4 (System), vol5 (Data), plus unallocated areas. Operating system iPhone OS 4.2.1 (8C148) from `SystemVersion.plist`.
- 49 EXIF-bearing carved images, several with GPS coordinates, timestamps and iPhone 3G identifiers (example: `f0136568.jpg`, created 2011-05-29 23:00:53 IST).
- Cookies recovered for domains including Facebook and Live.com.
- Email carved from unallocated space (vol5): a message from "Pat TeeSumTwelve" to `TracySumtwelve@gmail.com` ("Hey Sis, Thanks for the tickets…"). A "message-id" keyword search returned 8 results.
- **Assessment:** identity, timeline and location leads. No malicious action is established.

### Phone – Logical

- iPhone1,2 running iPhone OS 4.2.1 (AppleSupport `general.log`).
- `sms.db` holds 8 message records (numbers +15713083236, +17038296071, +12027252124). `call_history.db` holds 4 call records. **+15713083236 appears in both databases.**
- The Address Book contains Tracy, Pat, Terry, Carry and Apple Inc. No voicemail records were found.
- Application artefacts examined: Instagram, Facebook, FlashLight, Great Solitaire. Authentication and session values are not reproduced in this report.
- **Assessment:** communication and device evidence. It shows no malicious activity or user intent.

### Email

- Sender `root@Tracys-MacBook-Air.local`; recipient `joe.sum.twelve@gmail.com`; subject "Logfile"; date 29 Jun 2012 11:00:00 -0400.
- Sending IPv6 `2600:1003:b02a:3724:c15:34bf:4761:9c36`; received via `mx.google.com`; Message-ID `<20120629150000.3AAD564693@Tracys-MacBook-Air.local>`.
- SPF: Neutral. DKIM: not present. DMARC: not present (recorded as "not present", not "failed"). No URLs identified.
- The body contains LogKext daemon output, user account `tracysumtwelve`, login events at 09:14:10 and 10:33:25, and the address `coralbluetwo@hotmail.com`.
- **Assessment:** supports identity and timeline correlation. It does not establish a malicious action.

### Network

- 33,773 packets over about 24 hours. DHCP hostnames identify m57-jo (192.168.1.102), m57-pat (192.168.1.103), M57-Terry (192.168.1.105) and m57-charlie. 192.168.1.1 acts as gateway, DHCP and DNS.
- **Confirmed:** HTTP POSTs to `webmail.m57.biz` (208.97.187.139), URI `redirect.php`, content type `application/x-www-form-urlencoded`. The `login_username` and `secretkey` fields are readable in the payload. Terry submitted two login requests and Pat submitted one.
- 192.168.1.50 (MAC 00:0f:66:ae:e9:8a) shows a recurring DNS pattern (4.2.2.3, 4.2.2.4, 192.168.1.1, time/NTP-related names) across three captures. Its identity and purpose are unresolved.
- Recurring NBNS lookups for M57-CHARLIE were observed.
- **Assessment:** confirmed plaintext credential exposure. Interception or reuse is not shown.

## 4. Cross-Source Correlation

| **Correlation**                | **Evidence 1**                                       | **Evidence 2**                                                                   | **Strength**                                        |
|--------------------------------|------------------------------------------------------|----------------------------------------------------------------------------------|-----------------------------------------------------|
| Disk ↔ Network (host)          | Computer M57-JO, owner Jo                            | DHCP hostname m57-jo at 192.168.1.102                                            | Strong, direct                                      |
| Disk ↔ Network (share/gateway) | Z: → `\\192.168.1.1\m57`                             | 192.168.1.1 is gateway, DHCP and DNS                                             | Strong, infrastructure                              |
| Disk ↔ Memory                  | Jo / M57-JO, Windows XP SP3                          | Image named jo-2009-11-20, Z: path, Windows XP SP3                               | Supporting; no cryptographic link                   |
| Network ↔ Network              | 192.168.1.50 / MAC 00:0f:66:ae:e9:8a                 | Same IP, MAC and traffic signature in three captures                             | Direct persistence; identity unresolved             |
| Network ↔ Phone                | Hostnames m57-pat, M57-Terry                         | Contacts Pat and Terry                                                           | Supporting only; names do not prove the same people |
| Phone Logical (internal)       | +15713083236 in SMS                                  | +15713083236 in call history                                                     | Direct, intra-device                                |
| Phone Physical ↔ Email         | Carved email from Pat TeeSumTwelve to TracySumtwelve | Email artefacts referencing Tracy (`Tracys-MacBook-Air.local`, `tracysumtwelve`) | Potential identity cluster                          |
| Phone Physical ↔ Phone Logical | iPhone 3G identifiers in EXIF                        | iPhone1,2 model, OS 4.2.1                                                        | Consistent device identification                    |
| Network ↔ Memory               | LAN and webmail activity in PCAP                     | Empty memory network views                                                       | No event-level correlation                          |

The significant relationships are environmental (M57-JO ↔ m57-jo, Z: ↔ 192.168.1.1) and a device and identity cluster around Tracy's phone and MacBook. No relationship links the 2009 webmail credential exposure to the memory anomalies, the remote-management artefacts, or the 2012 phone and email evidence.

## 5. Supporting Evidence

1.  **Plaintext credentials (strongest).** Wireshark decodes the webmail logins as HTTP POST requests to `webmail.m57.biz` with the form fields readable at the application layer, for both Terry (192.168.1.105) and Pat (192.168.1.103). Supporting views: Figures 5–7 and 10 of Appendix A3. The PCAP hash is recorded.
2.  **Memory anomalies.** 7 Malfind and 12 Suspicious Threads findings (VolViewer Figures A6 and A7), with the process context in Figures A2–A5.
3.  **Host identification.** Autopsy Operating System Information (M57-JO, Jo, M57.biz) corroborated by the DHCP hostname m57-jo in the PCAP.
4.  **Shared-resource link.** Z: mapped to `\\192.168.1.1\m57` on disk, and 192.168.1.1 identified as gateway, DHCP and DNS in the PCAP.
5.  **Persistent unidentified host.** 192.168.1.50 with the same MAC and traffic pattern across three captures.
6.  **Remote-management artefacts.** Atera, Kaseya VSA and RDP on the disk (leads only).
7.  **Phone and email context.** The +15713083236 cross-database match, EXIF and GPS data, the carved Pat → Tracy email, and the "Logfile" EML with LogKext content.

## 6. Contradictions / Alternative Interpretations

- **Memory anomalies.** Non-file-backed VADs and `PAGE_READWRITE` regions can arise from dynamically allocated code in legitimate software. Flagged processes include core system processes (`csrss.exe`, `lsass.exe`) and an antivirus service (`avgwdsvc.exe`). Injection is possible, but heuristic false positives cannot be excluded.
- **`hkemd.exe`.** It is unidentified and notable, but there is no evidence establishing it as malicious or benign.
- **`cmd.exe` and `mdd_1.3.exe`.** These are consistent with the examiner's own acquisition, not attacker activity.
- **Remote-management tools (Atera, Kaseya, RDP).** These may be legitimate IT administration. The artefacts show presence and capability, not unauthorised use.
- **USB records.** Several entries are ordinary peripherals (mouse, keyboard). Flash drives and an external hard drive show device presence only, not any transfer.
- **Extension mismatches and password-protected archives.** These can occur through normal software behaviour or ordinary user practice.
- **192.168.1.50.** Its DNS queries to time and NTP-related names could suggest an infrastructure or utility device, but this is not established. It could equally be a system of interest.
- **LogKext in the email.** LogKext is a keystroke-logging tool, so the email contains captured keystrokes from the sending host. The evidence does not show who installed it or whether it was authorised or covert.
- **Names across sources.** Pat, Terry and Tracy appear in network hostnames, phone contacts and email addresses. Name matches alone do not prove they are the same individuals.
- **Chronology.** The PCAP (15 Nov 2009), memory and disk (20 Nov 2009) and phone and email (2011–2012) are separated in time, which weakens any single-narrative interpretation.

## 7. Evidence Limitations

- The identity and intent of any attacker cannot be established.
- Credential interception by a third party, mailbox compromise, and later reuse of the exposed credentials are not shown.
- The memory image has no usable network connection records, so the memory anomalies cannot be tied to any network activity.
- Malfind and Suspicious Threads results have not been validated against extracted memory regions, executable contents, persistence artefacts or disk evidence.
- 192.168.1.50 remains unidentified.
- Remote-management, USB and archive artefacts do not prove unauthorised access, transfer or concealment.
- Phone EXIF, cookies and carved email remnants need contextual interpretation, and phone numbers are not mapped to identities without corroboration.
- Hashes for the memory image and the two E01 files are not recorded in the supplied material.
- Time zones differ across sources (IST on disk, UTC in memory, EDT in the email) and have not been normalised into one timeline.
- The MxToolbox independent header analysis of the email is not documented as completed.
- Working-copy timestamps from the 2026 examination environment are not treated as original phone activity.

## 8. Final Forensic Assessment

The evidence supports one confirmed security event: webmail credentials for Terry and Pat were sent to `webmail.m57.biz` over unencrypted HTTP and were exposed in the captured network traffic. The root cause is webmail authentication being permitted without transport encryption.

The memory image is separately suspicious. Seven Malfind and twelve Suspicious Threads findings indicate anomalous memory regions, but these are indicators, not proof of malware or code injection.

The disk, phone and email evidence provide consistent host, user and device context, including strong environmental correlations (M57-JO ↔ m57-jo, Z: ↔ 192.168.1.1). None of them turns a lead into a confirmed malicious action. The evidence does not demonstrate credential interception, account takeover, unauthorised remote access, malware execution or data exfiltration, and it does not connect the 2009 credential exposure to the memory anomalies or the 2012 phone and email artefacts.

This assessment is confined to what the supplied evidence establishes. The items in Section 7 are the recommended next steps for validating the open leads.
