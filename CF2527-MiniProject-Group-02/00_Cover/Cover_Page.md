# Computer Forensics Mini Project

## Group 2 — Cipher Holmes

![Group 2 — Cipher Holmes](Group_Photo.jpeg)

### Case / Investigation Title
**M57**

### Course
Computer Forensics

### Faculty
Dr. Angelina Gokhale

### Group Members

| Sr. No. | Name | PRN. |
|---|---|---|
| 1 | Aparna Krishna | 25030241006 |
| 2 | Khushi Shaikh | 25030241023 |
| 3 | Sayali Shraddha | 25030241047 |
| 4 | Sumeet Upasani | 25030241103 |
| 5 | Preet Yadav | 25030241136 |

---

# Evidence Integrity

The following hashes were calculated for the evidence files investigated by the group.

| Sr. No. | Evidence Category | Evidence File | Hash Algorithm | Calculated Hash |
|---|---|---|---|---|
| 1 | Disk | `jo-2009-11-20-oldComputer.E01` | SHA-256 | `c141e380cb8e642dc5a905f253577dcf3dc205ebe97383ac00f2a18c6e3031cf` |
| 2 | Memory | `67210fe41fe5-jo-2009-11-20.mddramimage` | SHA-256 | *Not provided in supplied reports* |
| 3 | Phone – Physical | `tracy-phone-2012-07-05.E01` | SHA-256 | `7410eb756ed1af9e12d8d8873f9faa164076214a62a042d1b93b3d935e7333b7` |
| 4 | Phone – Logical | `tracy-phone-2012-07-05.tar` | SHA-256 | `aa8ac5304f5f12cf1eecb8462bd7aac5225f05ac42115bfebf5ad56befe86005` |
| 5 | Email | `logfile-2012-06-29-1100.eml` | SHA-256 | `43b6e813d69b09b6c8dc169e1ae88453b40d64fb396959aa7041c24084fc5fff` |
| 6 | Network | `net-2009-11-15-09_24.dmp` | SHA-256 | `f35e39a7d8533c07341ce490b9db00a93b5815e9defae87919d85425c9173a92` |

---

# Investigation Scope

Evidence sources investigated by the group:

- **Disk:** Windows XP SP3 drive image (`jo-2009-11-20-oldComputer.E01`) examined with Autopsy 4.23.1 — operating system and owner identification, 3,733 web-history records, 11 USB device events, Z: share mapping, and remote-management tool artefacts.
- **Memory:** Windows XP 32-bit memory image (`67210fe41fe5-jo-2009-11-20.mddramimage`) examined with VolViewer — process list/tree, command lines, 7 Malfind findings, 12 Suspicious Threads findings, registry hives and timeline.
- **Phone – Physical:** iPhone OS 4.2.1 physical image (`tracy-phone-2012-07-05.E01`) examined with Autopsy 4.23.1 — volume/partition layout, 49 EXIF-bearing carved images with GPS data, and carved email content recovered from unallocated space.
- **Phone – Logical:** Logical extraction of the same device (`tracy-phone-2012-07-05.tar`) — SMS (8 records), call history (4 records), contacts, calendar, application data and system/log artefacts.
- **Email:** Supplied `.eml` file (`logfile-2012-06-29-1100.eml`) examined for header and body artefacts — sender/recipient, sending IP, originating host, SPF/DKIM/DMARC results, LogKext daemon content and potential indicators of compromise.
- **Network:** Packet capture (`net-2009-11-15-09_24.dmp`, 33,773 packets, ~24 hours) examined with Wireshark — endpoint and DHCP hostname identification, DNS pattern analysis, and HTTP webmail login captures exposing plaintext credentials.

---

# Important Note

The findings documented in this case folder are based on the available forensic evidence.

Tool output has been interpreted and correlated before drawing conclusions.

Where evidence is insufficient to establish a conclusion, the limitation has been explicitly documented.
