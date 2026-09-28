# MEMORY FORENSICS — ARTEFACT ANALYSIS

## 1. Evidence Information

| Field | Details |
|---|---|
| Evidence Category | Memory |
| Evidence File | `67210fe41fe5-jo-2009-11-20.mddramimage` |
| Analyst | [Student Name] |
| Hash Algorithm | SHA-256 |
| Hash | Not provided in the VolViewer export |
| File Size | Not provided in the VolViewer export |
| Tool(s) Used | VolViewer examination workspace / Volatility-based plugins |

## 2. Objective

To examine the supplied Windows memory image for system context, process activity, command-line evidence, process relationships, suspicious memory regions, thread anomalies, registry-hive presence and available network information, and to correlate the findings across the VolViewer outputs.

## 3. Investigation Performed

### Tool / Technique

VolViewer examination reports were reviewed using the following plugin outputs:

- `windows.info.Info`
- `windows.pslist.PsList`
- `windows.psscan.PsScan`
- `windows.pstree.PsTree`
- `windows.cmdline.CmdLine`
- `windows.malfind.Malfind`
- `windows.suspicious_threads.SuspiciousThreads`
- `windows.threads.Threads`
- `windows.registry.hivelist.HiveList`
- `windows.netscan.NetScan`
- `windows.netstat.NetStat`
- Timeline output

### Artefact Examined

The evidence item is the memory image `67210fe41fe5-jo-2009-11-20.mddramimage`. The VolViewer reports identify the environment as Windows XP SP3, 32-bit, with `C:\WINDOWS` as the system root.

### Observation

The `Info` output records `NTBuildLab 2600.xpsp_sp3_gdr.090804-1435`, `NtMajorVersion 5`, `NtMinorVersion 1`, `Ts64Bit False`, `IsPAE False`, `KeNumberProcessors 1`, and system time `2009-11-21 00:07:30+00:00`.

The Process List and Process Scan outputs each report 38 timestamped process events. The process inventory includes Windows system processes, AVG security components, Java components, Outlook Express/Messenger and the processes `hkemd.exe`, `cmd.exe`, and `mdd_1.3.exe`.

The Command Lines output records:
- `C:\WINDOWS\system32\hkemd.exe` — PID 3724.
- `C:\WINDOWS\system32\cmd.exe` — PID 3228.
- `z:\ram\mdd_1.3.exe -o z:\ram\jo-2009-11-20.ram` — PID 2508.

The Process Tree output records `explorer.exe` PID 3332 and `msimn.exe` PID 2792, with two timestamped process-tree events.

Malfind reports **7 linked findings**. The linked findings have `CommitCharge 0`, no available timestamp, and are associated with VolViewer's Suspicious Threads analysis. Suspicious Threads reports **12 linked findings** and identifies VAD regions that are not backed by files and/or have an unexpected starting protection of `PAGE_READWRITE`. The named processes associated with the highlighted suspicious-thread findings include `csrss.exe` PID 916, `lsass.exe` PID 996, `avgwdsvc.exe` PID 1684 and `explorer.exe` PID 3332.

The Registry Hives output identifies user and system hives including `Jo\NTUSER.DAT`, `SOFTWARE`, `DEFAULT`, `SAM`, `SECURITY`, and `SYSTEM`.

The Network Scan and Network Status exports do not contain populated connection records; their chronology sections state that there are no timestamped events in the plugin result.

### Interpretation

The process and command-line evidence demonstrates that the memory image contains both normal system activity and a small set of processes that deserve contextual examination. The `mdd_1.3.exe` command is specifically structured to write a RAM image to `z:\ram\jo-2009-11-20.ram`, which is consistent with memory acquisition. It should not be interpreted as malicious solely because it is unusual.

The Malfind and Suspicious Threads outputs provide the strongest indicators of abnormal memory characteristics. Non-file-backed VAD regions and `PAGE_READWRITE` starting protection can be associated with injected or dynamically allocated code, but these indicators are heuristic and can also occur for legitimate reasons. The correct forensic conclusion is therefore that the processes/threads warrant deeper validation.

### Finding

The supplied memory image contains multiple forensic indicators that require further investigation, particularly the seven Malfind-linked findings and twelve Suspicious Threads findings. The evidence also documents command-line execution of `mdd_1.3.exe` and `cmd.exe` near the end of the captured activity.

## 4. Important Artefacts

| Artefact | Location / Identifier | Observation | Interpretation | Significance |
|---|---|---|---|---|
| System information | `Info` plugin | Windows XP SP3, 32-bit, one CPU; system time 2009-11-21 00:07:30 UTC | Establishes OS and capture context | High |
| Process inventory | `PsList` / `PsScan` | 38 timestamped process events | Provides process baseline and chronology | High |
| `hkemd.exe` | PID 3724 | Present under `C:\WINDOWS\system32\` | Requires contextual identification | Medium/High |
| `cmd.exe` | PID 3228 | Present in process list and command-line output | Indicates command-shell activity | Medium |
| `mdd_1.3.exe` | PID 2508 | Command writes RAM image to `z:\ram\jo-2009-11-20.ram` | Consistent with memory acquisition | High |
| Malfind findings | 7 linked findings | Non-file-backed / anomalous memory characteristics | Potential memory anomaly | High |
| Suspicious Threads | 12 linked findings | VADs not backed by files and/or `PAGE_READWRITE` protection | Potential thread/memory anomaly | High |
| Registry hives | `HiveList` | User and system hives recovered | Enables registry follow-up | Medium |
| Network status | `NetStat` / `NetScan` | No populated connection records | Network attribution unavailable from these exports | Limitation |

## 5. Evidence Supporting the Finding

The finding is supported by multiple independent VolViewer views:

1. **Process enumeration** establishes the existence and timing of the relevant processes.
2. **Command-line analysis** records the executable paths and the `mdd_1.3.exe` output command.
3. **Timeline analysis** corroborates the process/thread chronology.
4. **Malfind** identifies seven linked memory findings.
5. **Suspicious Threads** links twelve findings to VAD regions with anomalous characteristics.
6. **Registry Hive List** confirms that user and system registry evidence is available for further investigation.

## 6. Correlation With Other Evidence

| Evidence Source | Related Artefact | Relationship |
|---|---|---|
| Process List | `cmd.exe` PID 3228 | Supports |
| Process List | `mdd_1.3.exe` PID 2508 | Supports |
| Command Lines | `mdd_1.3.exe -o z:\ram\jo-2009-11-20.ram` | Supports |
| Timeline | `cmd.exe` / `mdd_1.3.exe` | Supports chronology |
| Malfind | Suspicious thread findings | Explicitly linked by VolViewer |
| Suspicious Threads | PIDs 916, 996, 1684, 3332 | Contextualises memory anomalies |
| Registry Hive List | `Jo\NTUSER.DAT`, `SYSTEM`, `SOFTWARE`, `SAM`, `SECURITY` | Contextualises possible follow-up analysis |
| Network Scan / Status | No populated records | Limits network correlation |

## 7. Limitations

- The original memory-image SHA-256 and file size are not included in the supplied VolViewer reports.
- The exported network views do not provide usable connection records.
- The supplied registry output lists hives but does not include registry-value analysis.
- Malfind and Suspicious Threads are indicators, not standalone proof of malicious code.
- The identity and intent of the user operating the system cannot be established from the supplied outputs.
- Some VolViewer exports are image-based examination worksheets, so interpretation relies on the visible report output rather than a raw plugin data export.

## 8. Conclusion

The memory image provides a coherent Windows XP SP3 process and thread environment and contains several notable forensic indicators. The most significant are the seven Malfind-linked findings, twelve Suspicious Threads findings, and the command-line evidence showing `cmd.exe` executing `mdd_1.3.exe` to create a RAM image. These findings justify deeper examination of the associated processes and memory regions, but the supplied evidence alone does not support a definitive conclusion that malware or an attacker was responsible.
