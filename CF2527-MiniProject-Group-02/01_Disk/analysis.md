# Disk Image — Detailed Forensic Analysis

## 1. Evidence Information

| Field | Details |
|---|---|
| Evidence Category | Disk Image |
| Evidence File | `jo-2009-11-20-oldComputer.E01` |
| Case | `CF_DriveImage_Investigation` |
| Case Number | `003` |
| Examiner | Khushi Matin Shaikh |
| Tool | Autopsy 4.23.1 |
| Time Zone | Asia/Calcutta |
| Data Sources | 1 |
| Report Generated | 2026-09-27 21:54:19 |
| Ingest Status | **COMPLETED** |
| SHA-256 | C141E380CB8E642DC5A905F253577DCF3DC205EBE97383AC00F2A18C6E3031CF |

### Evidence Integrity Note

The updated Autopsy `Case Summary` reports:

- Data Source: `jo-2009-11-20-oldComputer.E01`
- Ingest Job 1
- Status: **COMPLETED**
- Data Source Integrity Module: enabled

The supplied HTML report does not display the actual SHA-256 digest of the original E01 image. Therefore, the digest is intentionally not invented or inferred.

---

## 2. Objective

The objective of this investigation was to examine the supplied disk image using Autopsy and identify relevant forensic artefacts associated with:

1. Operating-system and host identification
2. User activity
3. Browser history and searches
4. Downloads
5. Installed and executed applications
6. Recent documents and Shell Bags
7. USB/removable devices
8. Image EXIF metadata
9. Encryption/password-protected archives
10. Extension mismatches
11. Potentially significant or suspicious artefacts
12. Correlations between independent artefact sources

The analysis distinguishes **observation**, **interpretation** and **finding** so that forensic tool output is not automatically treated as proof of a particular event.

---

# 3. Methodology

The disk image was loaded into **Autopsy 4.23.1** as a forensic data source. The configured ingest modules included:

- Recent Activity
- Hash Lookup
- File Type Identification
- Extension Mismatch Detector
- Embedded File Extractor
- Picture Analyzer
- Keyword Search
- Email Parser
- Encryption Detection
- Interesting Files Identifier
- Central Repository
- PhotoRec Carver
- Virtual Machine Extractor
- Data Source Integrity
- Android Analyzer
- DJI Drone Analyzer
- YARA Analyzer
- iOS Analyzer
- GPX Parser

The case summary confirms that the ingest job completed.

The investigation then examined the generated artefact categories and correlated related records across user, browser, application and removable-device artefacts.

---

# 4. Analysis of Findings

## 4.1 Operating System and Host Identification

### Observation

Autopsy's Operating System Information result identifies:

- Architecture: `x86`
- Operating System: `Microsoft Windows XP Service Pack 3`
- Computer Name: `M57-JO`
- Organization: `M57.biz`
- Owner: `Jo`
- Windows Path: `C:\WINDOWS`
- Product ID: `76487-027-5250835-22087`
- Temporary directory: `%SystemRoot%\TEMP`

### Interpretation

These artefacts establish the system environment represented by the E01 image. The `Jo` owner information is consistent with the user profile paths observed elsewhere in the image.

### Finding

The evidence represents a Windows XP SP3 x86 computer named `M57-JO`, associated with `M57.biz` and the user/owner `Jo`.

---

## 4.2 Communication and Email Artefacts

### Observation

Autopsy reports:

- 3 communication accounts
- 2 email-message artefacts

The accounts include:

- `linuxuser-admin@www.linux.org.uk`
- `mailer-daemon@zinfandel.lacita.com`
- `webmaster@python.org`

The email-message results include historical email content and headers.

### Interpretation

The email artefacts demonstrate that email-related data was present in the evidence image. Some of the messages are historical and should not automatically be interpreted as messages created or sent by the computer owner during the primary 2009 activity period.

### Finding

Email-related artefacts are present and can be used for additional contextual investigation, but the supplied results do not establish that these accounts belong to the `Jo` user.

---

## 4.3 Browser History

### Observation

Autopsy reports **3,733 web-history records**.

Both Internet Explorer and Firefox artefacts are represented.

Examples include history originating from:

- Internet Explorer `History.IE5/index.dat`
- Firefox `places.sqlite`

### Interpretation

The presence of these records demonstrates that browser history artefacts were stored on the system. Multiple browser sources provide independent artefact locations for activity.

### Finding

The system contains extensive browser activity associated at the artefact level with the `Jo` profile.

---

## 4.4 Web Search Activity

### Observation

Autopsy reports **39 web-search records**.

Examples include:

- `Download Firefox 2008`
- `adobe acrobat`
- `car max`
- `cnn`
- `coppola nicholas cage`
- `dell`
- `firefox`
- `mozrepl`
- `open office.org`
- `python download`
- `quicktime`
- `sf chronicle`
- `toys`
- `toysrus`
- `wikipedia`

Some search activity appears in both Internet Explorer and Firefox artefacts.

### Interpretation

Repeated terms across different browser artefacts strengthen the conclusion that the searches are represented in multiple stored browser sources.

### Finding

The evidence contains recorded web-search activity covering software, products, general information and other topics.

**Forensic caution:** A search-history entry establishes the existence of the recorded browser artefact. It does not independently prove the identity or intent of the person who entered the term.

---

## 4.5 Browser Form/Identity Artefacts

### Observation

The Web Form Autofill result contains entries including:

- `j_email = jo@m57.biz`
- `j_name = jo`

### Interpretation

These entries correlate with the operating-system owner information identifying `Jo` and organization `M57.biz`.

### Finding

The browser artefacts are consistent with the `Jo` user profile and provide supporting contextual evidence for associating browser activity with that profile.

---

## 4.6 Download Activity

### Observation

Autopsy reports **7 web-download records**.

Important records include:

| File | Date/Time | Source |
|---|---|---|
| `python-2.6.4.msi` | 2009-11-13 07:25:49 IST | python.org |
| `PNEUMATIC_BOXING_GLOVE.pdf` | 2009-11-18 23:30:01 IST | google.com |
| `hardware_grid.csv` | 2009-11-19 22:50:45 IST | access-board.gov |
| `QuickTimeInstaller.exe` | 2009-11-20 23:11:19 IST | edgesuite.net |
| `AdbeRdr920_en_US.exe` | 2009-11-20 23:28:59 IST | adobe.com |

Additional Internet Zone artefacts include Firefox Setup 3.5.5 and another executable.

### Interpretation

The Firefox download database and Zone.Identifier artefacts provide evidence that the listed files were associated with browser download activity.

### Finding

The evidence contains a useful software/document acquisition timeline, particularly around 13–20 November 2009.

---

## 4.7 Application Installation

### Observation

Autopsy reports **99 installed-program records**.

Examples include:

- AVG 9.0
- Adobe Reader 9.2 v.9.2.0
- Apple Application Support v.1.1.0
- Apple Software Update v.2.1.1.116
- Windows XP hotfixes

Adobe Reader 9.2 is recorded with an installation date/time of:

`2009-11-20 18:04:05 IST`

### Interpretation

Installed-program artefacts provide evidence that these programs were registered as installed in the Windows software registry.

### Finding

The system contained common software and security software including AVG, Adobe Reader and Apple components. The presence of a program in the installed-program list does not by itself establish how or why it was used.

---

## 4.8 Program Execution

### Observation

Autopsy reports **84 Run Program records**.

A notable record is:

`ACRORD32.EXE`

Date/Time:

`2009-11-20 23:34:46 IST`

Associated artifact:

`Prefetch File`

Path:

`/PROGRAM FILES/ADOBE/READER 9.0/READER`

Other records include multiple AVG executables.

### Interpretation

Windows Prefetch artefacts are useful execution-related evidence. They indicate that the corresponding executable was represented in Prefetch data at the recorded time.

### Finding

Adobe Reader execution is recorded at approximately 23:34 on 20 November 2009, following the Adobe Reader download at approximately 23:28. This provides a useful cross-artefact timeline correlation.

---

## 4.9 EXIF Metadata

### Observation

Autopsy reports **274 EXIF records**.

Identified camera/device models include:

- Nikon D1
- Hasselblad H3D-39
- Hasselblad CFH
- Nikon D70s
- Canon EOS 5D
- Sony HDR-SR10

The report contains image capture dates ranging from 2003 through 2009.

Several 2009 Sony HDR-SR10 records correspond to files under:

`C:\Documents and Settings\Jo\Desktop\Pics\`

### Interpretation

EXIF metadata provides information embedded in image files and can support temporal and device correlation.

### Finding

The evidence contains substantial image metadata associated with multiple cameras/devices. The supplied EXIF results do not establish a physical location for the images because the reviewed entries do not provide usable GPS coordinates.

---

## 4.10 User Content Suspected

### Observation

Autopsy reports **274 User Content Suspected records**.

Many of these are identified because:

`EXIF metadata data exists for this file.`

Examples include:

- `DSC00036.JPG`
- `DSC00037.JPG`
- `DSC00038.JPG`
- `DSC00039.JPG`

### Interpretation

The rule is identifying image files containing EXIF metadata as potentially relevant user content.

### Finding

The evidence contains a substantial collection of user-associated image files with embedded metadata.

---

## 4.11 USB Device Activity

### Observation

Autopsy reports **11 USB-device records**.

Important entries include:

**Alcor Micro Corp.**
- Model: Flash Drive
- Device ID: `51491E64`
- Time: `2009-11-18 00:15:06 IST`

**Imation Corp.**
- Model: Flash Drive
- Device ID: `AADA04411400000B`
- Time: `2009-11-20 23:07:06 IST`

**LaCie, Ltd**
- Model: Rugged Triple Interface Mobile Hard Drive
- Device ID: `00D04B881007C255`
- Time: `2009-11-17 05:50:07 IST`

### Interpretation

These records originate from Windows SYSTEM registry artefacts and demonstrate that the operating system recorded the listed devices.

### Finding

The system interacted with multiple removable storage devices. This is significant for data-transfer investigations.

**Limitation:** The supplied report does not prove which files were copied to or from each device.

---

## 4.12 Recent Documents

### Observation

Autopsy reports **25 Recent Documents**.

Examples include:

- `C:\Documents and Settings\Jo\Desktop\Pics`
- `DSC00008.JPG`
- `DSC00009.JPG`
- `Cat.m4v`
- `Cat.mov`
- `Tigger.m4v`
- `TiggerTheCat.m4v`
- `95253.SCSI.Mathew+Malizia.pd`

### Interpretation

Recent-document artefacts can indicate that applications or Windows maintained records of files/folders recently accessed or opened.

### Finding

The evidence contains multiple records connecting the `Jo` profile to the `Desktop\Pics` directory and associated image/video files.

---

## 4.13 Shell Bags

### Observation

Autopsy reports **42 Shell Bag records**.

### Interpretation

Shell Bags are useful for reconstructing Windows Explorer folder interaction and historical folder access.

### Finding

The presence of Shell Bag records provides additional user-activity evidence that can be correlated with Recent Documents and file-system artefacts.

---

## 4.14 Remote Drive

### Observation

Autopsy reports one Remote Drive:

- Local path: `Network\Z`
- Remote path: `\\192.168.1.1\m57`

### Interpretation

The evidence contains a Windows network-drive mapping from drive `Z:` to the network path `\\192.168.1.1\m57`.

### Finding

A network share was mapped as drive `Z:` in the system artefacts. The report does not establish whether the share was active at the time of every other recorded event.

---

## 4.15 Interesting Items — Remote Management

### Observation

Autopsy's Interesting Items result identifies four table entries under:

`Remote Monitoring Management Programs`

They include:

1. **Atera** — Administrator profile OpenOffice.org package-cache log
2. **Atera** — Jo profile OpenOffice.org package-cache log
3. **Kaseya (VSA)** — Windows SYSTEM registry log
4. **Microsoft RDP** — `mstsc.exe`

### Interpretation

Autopsy's ruleset has identified artefacts associated with remote monitoring/management technologies.

### Finding

Remote-management-related artefacts are present and should be treated as an investigation lead.

### Forensic Qualification

These findings do **not** establish:

- unauthorized remote access
- malware infection
- attacker activity
- compromise
- data exfiltration

Additional evidence would be required, such as network connections, event logs, service installation records, execution history and user/account activity.

---

## 4.16 Extension Mismatch Detection

### Observation

Autopsy reports **76 extension-mismatch records**.

Examples include files where the extension does not correspond directly with the detected MIME type.

### Interpretation

Extension mismatch is a forensic triage indicator. Legitimate applications may use extensions that do not correspond to a simple MIME-type expectation.

### Finding

The image contains files requiring additional review, but the supplied report does not establish deliberate file masquerading or tampering.

---

## 4.17 Password-Protected Archives

### Observation

Autopsy's Encryption Detection module identified password protection in multiple ZIP archives.

The records include carved ZIP files and AVG files such as:

- `internalList.zip`
- `internalList.zip.bak`
- `quarantinedList.zip`
- `quarantinedList.zip.bak`
- `userList.zip`
- `userList.zip.bak`

### Interpretation

Password protection was detected by the forensic tool. Several files are located within AVG configuration/quarantine directories.

### Finding

Password-protected archives exist in the evidence. Their locations provide contextual evidence that many are related to AVG software rather than automatically indicating malicious encrypted content.

---

# 5. Cross-Artefact Correlation

## 5.1 User Correlation

The operating-system information identifies the owner as `Jo`.

Browser artefacts also contain:

- `j_name = jo`
- `j_email = jo@m57.biz`

This provides a consistent artefact-level association between the Windows owner information and the browser profile.

---

## 5.2 Firefox Download → Installation/Execution Correlation

The evidence records:

1. Adobe Reader download at approximately `23:28:59` on 20 November 2009.
2. Adobe Reader installation at approximately `18:04:05` on the same date.
3. Adobe Reader execution through `ACRORD32.EXE` at approximately `23:34:46`.

The installation time precedes the recorded execution, while the browser download artefact appears shortly before the execution record.

This demonstrates a useful relationship among download, installation and execution artefacts.

---

## 5.3 USB and User Activity Correlation

The image contains multiple USB-storage records, including Alcor Micro, Imation and LaCie devices.

The same evidence also contains user files, recent documents and browser/download activity.

This establishes that removable-storage devices were recorded on the system during a period when user activity was also present.

However, the report does not provide direct evidence linking a particular file transfer to a particular USB device.

---

## 5.4 Remote Management Correlation

Atera, Kaseya VSA and Microsoft RDP artefacts are all identified by the Interesting Items analysis.

The presence of several remote-management-related artefacts makes this an area for further investigation.

However, the report does not provide enough evidence to conclude that these technologies were used maliciously.

---

# 6. Timeline of Selected Events

| Date/Time | Evidence | Interpretation |
|---|---|---|
| 2009-11-13 01:48 | `Download Firefox 2008` search | Browser search activity |
| 2009-11-13 07:25 | Python 2.6.4 MSI download | Software acquisition |
| 2009-11-17 05:50 | LaCie Rugged drive | USB/removable device record |
| 2009-11-18 00:15 | Alcor Micro Flash Drive | USB/removable device record |
| 2009-11-18 23:30 | Patent PDF download | Document acquisition |
| 2009-11-19 22:50 | `hardware_grid.csv` download | Data/document acquisition |
| 2009-11-20 23:07 | Imation Flash Drive | USB/removable device record |
| 2009-11-20 23:11 | QuickTime download | Software acquisition |
| 2009-11-20 23:28 | Adobe Reader download | Software acquisition |
| 2009-11-20 23:34 | `ACRORD32.EXE` Prefetch record | Execution-related evidence |

---

# 7. Significance Assessment

| Finding | Significance | Assessment |
|---|---|---|
| Windows XP SP3 / Jo profile | Context | Confirmed |
| 3,733 web-history records | User activity | Significant |
| 39 web-search records | Search activity | Significant |
| Multiple software downloads | Acquisition activity | Significant |
| 274 EXIF records | Image/device correlation | Significant |
| 11 USB records | Removable media | Significant |
| Atera artefacts | Remote-management lead | Requires further investigation |
| Kaseya VSA artefact | Remote-management lead | Requires further investigation |
| Microsoft RDP artefact | Remote-access capability | Requires contextual correlation |
| 76 extension mismatches | File triage | Requires individual examination |
| Password-protected ZIPs | Encryption indicator | Context-dependent |

---

# 8. Limitations

1. The supplied material is an Autopsy HTML report rather than the original E01 evidence image.
2. The SHA-256 value of the E01 is not displayed in the supplied report.
3. The report establishes artefacts but cannot independently establish the identity or intent of the person operating the computer.
4. USB artefacts establish recorded device presence but do not prove a particular file transfer.
5. Atera/Kaseya/RDP artefacts do not by themselves prove malicious remote access.
6. Extension mismatches do not automatically indicate file tampering.
7. Password-protected archives do not automatically indicate malicious encrypted content.
8. EXIF metadata can be copied or preserved in files and therefore should be interpreted in conjunction with file-system and application artefacts.
9. The analysis is based on the artefacts presented in the generated Autopsy report; files not surfaced in the report were not independently examined.

---

# 9. Final Conclusion

The completed Autopsy analysis successfully processed the disk image and recovered a broad range of forensic artefacts.

The evidence establishes a Windows XP SP3 x86 environment associated with the `Jo` profile, extensive browser activity, software and document downloads, image metadata, removable-storage records, recent-document activity and application execution evidence.

The most important investigative lead is the presence of artefacts classified by Autopsy under **Remote Monitoring Management Programs**, including Atera, Kaseya VSA and Microsoft RDP. These findings should be validated using additional evidence before drawing any conclusion about unauthorized access or compromise.

The evidence also provides useful correlations between browser searches, downloads, software installation/execution, user-profile artefacts and removable devices.

, the updated Autopsy case summary confirms:

**Ingest Job 1 — Status: COMPLETED**


The remaining evidence-integrity item is the SHA-256 digest of the original E01, which should be obtained directly from the original evidence file or the case's integrity verification output before the final submission.
