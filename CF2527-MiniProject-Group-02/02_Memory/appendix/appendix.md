# APPENDIX — COMPUTER FORENSICS / MEMORY FORENSICS

## Supporting Screenshots and Evidence

This appendix contains the VolViewer evidence-analysis screenshots and report references used during the memory-forensics investigation.

### Appendix A — VolViewer Evidence-Analysis Screenshots

These figures document the major stages of the memory examination.

**Figure A1.** VolViewer `Info` output showing the Windows XP SP3 / 32-bit system context and recorded system time.  
**Source:** `VolViewer-Info.pdf`, page 2.

**Figure A2.** VolViewer Process List showing the process inventory and creation/exit-time information, including `hkemd.exe`, `cmd.exe` and `mdd_1.3.exe`.  
**Source:** `VolViewer-ProcessList.pdf`, page 2.

**Figure A3.** VolViewer Process Scan providing the cross-checked process enumeration, including `mdd_1.3.exe` PID 2508 and `cmd.exe` PID 3228.  
**Source:** `VolViewer-ProcessScan.pdf`, page 2.

**Figure A4.** VolViewer Process Tree showing the process relationships for `explorer.exe` and `msimn.exe`, with the corresponding chronology.  
**Source:** `VolViewer-ProcessTree.pdf`, pages 2–3.

**Figure A5.** VolViewer Command Lines output showing executable paths and the command used by `mdd_1.3.exe` to write a RAM image.  
**Source:** `VolViewer-CommandLines.pdf`, pages 2–3.

**Figure A6.** VolViewer Malfind output showing 7 linked findings associated with suspicious memory characteristics.  
**Source:** `VolViewer-Malfind.pdf`, pages 2–3.

**Figure A7.** VolViewer Suspicious Threads output showing 12 linked findings and VAD-related anomalies, including non-file-backed regions and unexpected `PAGE_READWRITE` protection.  
**Source:** `VolViewer-SuspiciousThreads.pdf`, pages 2–4.

**Figure A8.** VolViewer Registry Hives output showing recovered user and system registry hives.  
**Source:** `VolViewer-RegistryHives.pdf`, page 2.

**Figure A9.** VolViewer Threads output containing the detailed thread enumeration used as supporting context for the suspicious-thread analysis.  
**Source:** `VolViewer-Threads.pdf`, pages 2–23.

**Figure A10.** VolViewer Timeline output documenting process and thread chronology across the memory examination.  
**Source:** `VolViewer-Timeline.pdf`, 272-page timeline export.

**Figure A11.** VolViewer Network Scan output. The exported view does not contain populated connection records.  
**Source:** `VolViewer-NetworkScan.pdf`, page 2.

**Figure A12.** VolViewer Network Status output. The exported view does not contain populated connection records or timestamped events.  
**Source:** `VolViewer-NetworkStatus.pdf`, pages 2–3.

### Appendix B — Key Evidence Reference

| Evidence Item | Reference |
|---|---|
| Memory image | `67210fe41fe5-jo-2009-11-20.mddramimage` |
| OS | Windows XP SP3 / NT 5.1 / build 2600 |
| Architecture | 32-bit; `Ts64Bit False`; `IsPAE False` |
| Processor count | 1 |
| Recorded system time | `2009-11-21 00:07:30+00:00` |
| Process events | 38 timestamped events |
| Malfind findings | 7 linked findings |
| Suspicious Threads | 12 linked findings |
| Network Scan / Status | No populated results in supplied exports |
| Memory-image SHA-256 | Not provided in the supplied VolViewer reports |

### Appendix C — Key Process / Timeline References

| Time (UTC) | Artefact | PID | Relevance |
|---|---|---:|---|
| 2009-11-20 19:59:50 | `explorer.exe` | 3332 | User-session process context |
| 2009-11-20 20:00:26 | `hkemd.exe` | 3724 | Process requiring contextual identification |
| 2009-11-20 22:16:17 | `msimn.exe` | 2792 | Outlook Express process-tree event |
| 2009-11-21 00:07:03 | `cmd.exe` | 3228 | Command-shell activity |
| 2009-11-21 00:07:29 | `mdd_1.3.exe` | 2508 | RAM-image acquisition command |

### Appendix D — Interpretation Note

The VolViewer `Malfind` and `Suspicious Threads` outputs should be treated as **forensic indicators** rather than definitive malware identification. The strongest defensible statement from the supplied evidence is that several processes contained memory/thread characteristics that VolViewer flagged for investigation. Further validation would require examining the associated memory regions, executable contents, persistence artefacts, and any available network or disk evidence.
