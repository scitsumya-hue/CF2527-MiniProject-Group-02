# Disk Image — Investigation Summary

## 1. Case and Evidence Information

| Field | Details |
|---|---|
| Case Name | `CF_DriveImage_Investigation` |
| Case Number | `003` |
| Evidence File | `jo-2009-11-20-oldComputer.E01` |
| Evidence Type | Disk Image |
| Data Sources | 1 |
| Examiner | Khushi Matin Shaikh |
| Autopsy Version | 4.23.1 |
| Report Generated | 2026-09-27 21:54:19 |
| Time Zone | Asia/Calcutta |
| Evidence Path | `C:\Users\khush\Downloads\jo-2009-11-20-oldComputer.E01` |
| Ingest Job Status | **COMPLETED** |
| SHA-256 | Not present in the supplied HTML report |

> **Integrity note:** The updated Autopsy report shows the Data Source Integrity module was enabled and the ingest job status is **COMPLETED**. However, the supplied HTML report does not display the SHA-256 value of the original E01 image. Therefore, no hash value is inserted here.

---

## 2. Executive Summary

The forensic examination was performed on the disk image `jo-2009-11-20-oldComputer.E01` using Autopsy 4.23.1. The evidence contains a Microsoft Windows XP Service Pack 3 x86 system identified as `M57-JO`, associated with the organization `M57.biz` and owner/user `Jo`.

The completed Autopsy ingest produced operating-system, browser, email, application, removable-device, file-system, EXIF and other forensic artefacts. Significant results include extensive web activity, browser searches, downloads, image EXIF metadata, USB-device records, recent-document activity, Shell Bags, extension mismatches, password-protected archives and remote-management-related artefacts.

The most notable triage finding is that Autopsy's **Remote Monitoring Management Programs** rule identified artefacts associated with **Atera**, as well as entries associated with Kaseya (VSA) and Microsoft RDP. These findings indicate the presence of remote-management-related artefacts, but they do **not by themselves prove malicious activity or unauthorized access**.

The updated report is materially different from the earlier report because the Autopsy case summary now states:

**Ingest History — Job 1 — Status: COMPLETED**

Therefore, the previous limitation that the report had been generated before ingest services completed should **not** be carried forward into the final analysis.

---

## 3. Key Artefact Statistics

The following counts are taken from the generated Autopsy report:

- **Communication Accounts:** 3
- **E-Mail Messages:** 2
- **Installed Programs:** 99
- **Metadata:** 337
- **Operating System Information:** 1
- **Recent Documents:** 25
- **Remote Drive:** 1
- **Run Programs:** 84
- **Shell Bags:** 42
- **USB Device Attached:** 11
- **Web Bookmarks:** 96
- **Web Cookies:** 310
- **Web Downloads:** 7
- **Web Form Autofill:** 10
- **Web History:** 3,733
- **Web Search:** 39
- **EXIF Metadata:** 274
- **Extension Mismatch Detected:** 76
- **User Content Suspected:** 274
- **Interesting Items:** 4 table entries
- **Encryption Detected:** 12 password-protected archive entries

---

## 4. Major Findings

### 4.1 Operating System and Host

Autopsy identified:

- Operating System: **Microsoft Windows XP Service Pack 3**
- Architecture: **x86**
- Computer name: **M57-JO**
- Organization: **M57.biz**
- Owner: **Jo**
- Windows directory: `C:\WINDOWS`

These artefacts establish the operating-system and host context of the evidence image.

---

### 4.2 Browser Activity

The image contains extensive browser artefacts from both **Internet Explorer** and **Mozilla Firefox**.

Autopsy reported:

- 3,733 web-history records
- 39 web-search records
- 310 cookies
- 96 bookmarks
- 10 web-form/autofill records

Examples of recorded searches include:

- `Download Firefox 2008`
- `adobe acrobat`
- `car max`
- `cnn`
- `coppola nicholas cage`
- `dell`
- `firefox`
- `mozrepl`
- `python download`
- `quicktime`
- `sf chronicle`
- `toys`
- `toysrus`
- `wikipedia`

The records demonstrate that corresponding browser history/search entries existed. A stored search term alone should not be interpreted as proof of a user's intent.

---

### 4.3 Download Activity

The report identifies several downloads associated with the `Jo` Firefox profile, including:

| File | Date/Time | Domain |
|---|---|---|
| `python-2.6.4.msi` | 2009-11-13 07:25:49 IST | python.org |
| `PNEUMATIC_BOXING_GLOVE.pdf` | 2009-11-18 23:30:01 IST | google.com |
| `hardware_grid.csv` | 2009-11-19 22:50:45 IST | access-board.gov |
| `QuickTimeInstaller.exe` | 2009-11-20 23:11:19 IST | edgesuite.net |
| `AdbeRdr920_en_US.exe` | 2009-11-20 23:28:59 IST | adobe.com |

The report also contains Zone.Identifier artefacts for Firefox Setup 3.5.5 and another executable.

---

### 4.4 EXIF Metadata

Autopsy identified **274 EXIF records**.

Device manufacturers/models appearing in the report include:

- NIKON CORPORATION — NIKON D1
- NIKON CORPORATION — NIKON D70s
- Hasselblad — Hasselblad H3D-39
- Hasselblad — Hasselblad CFH
- Canon — Canon EOS 5D
- SONY — HDR-SR10

Several records contain image capture timestamps. The supplied EXIF results do not provide GPS values for the examples reviewed, so no location conclusion is made from them.

---

### 4.5 Remote-Management-Related Artefacts

Autopsy's Interesting Items result identified:

| Rule | Associated Program | Artefact |
|---|---|---|
| Remote Monitoring Management Programs | Atera | Administrator OpenOffice.org package-cache `log.txt` |
| Remote Monitoring Management Programs | Atera | Jo OpenOffice.org package-cache `log.txt` |
| Remote Monitoring Management Programs | Kaseya (VSA) | `WINDOWS/system32/config/system.LOG` |
| Remote Monitoring Management Programs | Microsoft RDP | `WINDOWS/system32/mstsc.exe` |

These are important triage artefacts.

**Interpretation:** They indicate that Autopsy's ruleset recognized artefacts associated with remote-management software or functionality.

**Qualification:** Their presence alone does not establish compromise, malicious use, or unauthorized remote access. Further correlation would be required with execution history, installation records, network artefacts and event logs.

---

### 4.6 USB Devices

Autopsy reported **11 USB-device records**.

Notable entries include:

- **Alcor Micro Corp. — Flash Drive**
  - Device ID: `51491E64`
  - Date/Time: `2009-11-18 00:15:06 IST`
- **Imation Corp. — Flash Drive**
  - Device ID: `AADA04411400000B`
  - Date/Time: `2009-11-20 23:07:06 IST`
- **LaCie, Ltd — Rugged Triple Interface Mobile Hard Drive**
  - Device ID: `00D04B881007C255`
  - Date/Time: `2009-11-17 05:50:07 IST`
- Dell Model L100 Keyboard
- Logitech Optical Wheel Mouse

These records show that Windows retained evidence of recognition/attachment of removable devices.

---

### 4.7 Recent Documents and Shell Bags

Autopsy reported:

- 25 Recent Documents
- 42 Shell Bag records

Examples include:

- `C:\Documents and Settings\Jo\Desktop\Pics`
- `DSC00008.JPG`
- `DSC00009.JPG`
- `Cat.m4v`
- `Cat.mov`
- `Tigger.m4v`
- `TiggerTheCat.m4v`
- `95253.SCSI.Mathew+Malizia.pd`

These artefacts help reconstruct user interaction with files and folders.

---

### 4.8 Extension Mismatch

Autopsy reported **76 extension-mismatch records**.

Examples include files where the detected MIME type differs from the filename extension.

**Finding:** These records are useful for triage and may justify examination of individual files. They do not, by themselves, establish that files were deliberately disguised or modified.

---

### 4.9 Password-Protected Archives

Autopsy's Encryption Detection module identified password protection in multiple ZIP archives.

The report includes:

- Carved `internalList.zip` files
- AVG `internalList.zip`
- AVG `internalList.zip.bak`
- AVG `quarantinedList.zip`
- AVG `quarantinedList.zip.bak`
- AVG `userList.zip`
- AVG `userList.zip.bak`

The paths strongly associate many of these archives with AVG configuration/quarantine data.

---

## 5. Correlated Timeline Highlights

| Date/Time | Artefact | Significance |
|---|---|---|
| 2009-11-13 01:48–07:25 | Firefox-related searches and Python download | Browser activity and software acquisition |
| 2009-11-17 05:50 | LaCie Rugged external drive recorded | Removable-storage artefact |
| 2009-11-18 00:15 | Alcor Micro flash drive recorded | Removable-storage artefact |
| 2009-11-18 23:30 | Patent PDF downloaded | Document acquisition |
| 2009-11-19 22:50 | `hardware_grid.csv` downloaded | Document/data acquisition |
| 2009-11-20 23:07 | Imation flash drive recorded | Removable-storage artefact |
| 2009-11-20 23:11 | QuickTime downloaded | Software acquisition |
| 2009-11-20 23:28 | Adobe Reader downloaded | Software acquisition |
| 2009-11-20 23:34 | Adobe Reader executed according to Prefetch | Execution artefact |

The timestamps should be treated as artefact-specific times rather than automatically assuming that every event represents direct human action.

---

## 6. Overall Conclusion

The completed Autopsy examination of `jo-2009-11-20-oldComputer.E01` produced a substantial set of forensic artefacts covering operating-system information, browser activity, downloads, user activity, EXIF metadata, USB devices, application execution and remote-management-related indicators.

The strongest observations are the extensive Internet activity associated with the `Jo` profile, multiple software/document downloads, evidence of removable storage devices, extensive image metadata and the presence of artefacts recognized by Autopsy as Atera, Kaseya (VSA) and Microsoft RDP-related remote-management items.

The Atera/Kaseya/RDP findings should be treated as **investigative leads**, not as proof of malicious activity. The supplied report does not independently establish unauthorized remote access.

Most importantly, the updated Autopsy case summary confirms that **Ingest Job 1 completed successfully**. Therefore, the earlier warning that the report was generated before ingest services completed is no longer applicable to this updated report.

The SHA-256 value of the original E01 is not displayed in the supplied HTML report and should be obtained directly from the original evidence image or the case's integrity verification output before final submission.
