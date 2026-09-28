# MEMORY FORENSICS — INVESTIGATION SUMMARY

## Evidence Files Investigated

| File | Analyst | Hash |
|---|---|---|
| `67210fe41fe5-jo-2009-11-20.mddramimage` | [Student Name] | Not provided in the VolViewer export |

**Supporting VolViewer reports examined:** Info, Process List, Process Scan, Process Tree, Command Lines, Malfind, Suspicious Threads, Threads, Registry Hives, Network Scan, Network Status and Timeline.

## Summary Statistics

- **Evidence item:** 1 memory image represented by the VolViewer examination reports.
- **VolViewer reports examined:** 12.
- **Process events:** 38 timestamped events in both Process List and Process Scan.
- **Malfind findings:** 7 linked findings.
- **Suspicious-thread findings:** 12 linked findings.
- **Network Scan / Network Status:** exported views contained no populated results or timestamped events.
- **Operating system context:** Windows XP SP3, 32-bit, one processor; system time recorded as `2009-11-21 00:07:30+00:00`.

## Files / Artefacts Investigated

### 1. System Information

**Source:** `VolViewer-Info.pdf`

**Investigation:** Examined the VolViewer `Info` plugin output to establish the memory-image operating-system and system context.

**Finding:** The image represents a Windows XP SP3 environment (`NT 5.1`, build 2600), 32-bit, non-PAE, with one processor. The system root is `C:\WINDOWS` and the recorded system time is `2009-11-21 00:07:30+00:00`.

### 2. Process Activity

**Source:** `VolViewer-ProcessList.pdf`, `VolViewer-ProcessScan.pdf`

**Investigation:** Compared process enumeration outputs and their chronology.

**Finding:** 38 timestamped process events were reported. The process set includes normal Windows components, AVG security processes, Java components, Outlook Express/Messenger, `hkemd.exe`, `cmd.exe`, and `mdd_1.3.exe`. The presence of `cmd.exe` and `mdd_1.3.exe` near the end of the recorded activity is particularly relevant.

### 3. Command-Line Evidence

**Source:** `VolViewer-CommandLines.pdf`

**Investigation:** Reviewed command-line records associated with processes.

**Finding:** The image contains command lines for `hkemd.exe` (PID 3724) and a memory-acquisition command:
`z:\ram\mdd_1.3.exe -o z:\ram\jo-2009-11-20.ram` (PID 2508), launched from `cmd.exe` (PID 3228). This demonstrates that a memory-dumping utility was present in the captured environment; the command alone does not establish malicious intent.

### 4. Process Relationships

**Source:** `VolViewer-ProcessTree.pdf`

**Investigation:** Reviewed the process-tree relationships and chronology.

**Finding:** `explorer.exe` (PID 3332) and `msimn.exe` (PID 2792) are shown in the process tree. The exported chronology records two process-tree events: `explorer.exe` at `2009-11-20T19:59:50+00:00` and `msimn.exe` at `2009-11-20T22:16:17+00:00`.

### 5. Memory Anomalies

**Source:** `VolViewer-Malfind.pdf`, `VolViewer-SuspiciousThreads.pdf`

**Investigation:** Examined VolViewer's Malfind and Suspicious Threads outputs and their linked findings.

**Finding:** Malfind reports 7 linked findings, while Suspicious Threads reports 12 linked findings. The suspicious-thread output identifies threads whose VAD regions were not backed by files and/or had unexpected starting protection of `PAGE_READWRITE`. The findings are associated with processes including `csrss.exe` (PID 916), `lsass.exe` (PID 996), `avgwdsvc.exe` (PID 1684) and `explorer.exe` (PID 3332). These are indicators requiring further investigation, but they do not by themselves prove code injection or malware.

### 6. Registry Evidence

**Source:** `VolViewer-RegistryHives.pdf`

**Investigation:** Reviewed the registry-hive list recovered from memory.

**Finding:** The image contains user and system registry hives including `Jo\NTUSER.DAT`, `SOFTWARE`, `DEFAULT`, `SAM`, `SECURITY`, and `SYSTEM`, along with LocalService and NetworkService hives. The hive-list output alone does not establish persistence or a specific registry modification.

### 7. Thread and Timeline Evidence

**Source:** `VolViewer-Threads.pdf`, `VolViewer-Timeline.pdf`

**Investigation:** Reviewed the thread enumeration and the exported chronology.

**Finding:** The timeline corroborates process and thread activity, including the presence of `cmd.exe` and `mdd_1.3.exe` at approximately `00:07:03` and `00:07:29` on 21 November 2009. The thread output provides the underlying thread-level context used by the Suspicious Threads analysis.

### 8. Network-Related Memory Views

**Source:** `VolViewer-NetworkScan.pdf`, `VolViewer-NetworkStatus.pdf`

**Investigation:** Reviewed the exported network-scan and network-status plugin views.

**Finding:** The exported views do not contain populated connection records or timestamped events. Therefore, the memory reports do not independently establish a network connection or remote endpoint from these two plugins.

## Consolidated Findings

1. The examined memory image represents a Windows XP SP3, 32-bit environment with one processor and a recorded system time of `2009-11-21 00:07:30+00:00`.
2. Process enumeration identified 38 timestamped process events, including normal system/security software and notable processes such as `hkemd.exe`, `cmd.exe`, and `mdd_1.3.exe`.
3. Seven Malfind-linked findings and twelve Suspicious Threads findings indicate memory regions/threads with characteristics that VolViewer flags as anomalous, including non-file-backed VADs and unexpected `PAGE_READWRITE` protection.
4. The command-line and timeline evidence show `mdd_1.3.exe` executing with an output path for a RAM image. This is consistent with memory-acquisition activity, but the evidence provided does not by itself attribute the activity to an attacker.
5. The exported Network Scan and Network Status views do not provide usable connection evidence.

## Correlations

- `cmd.exe` PID 3228 and `mdd_1.3.exe` PID 2508 appear in both process enumeration and command-line evidence.
- The Timeline corroborates the late-stage appearance of `cmd.exe` and `mdd_1.3.exe`.
- Malfind findings are explicitly linked by VolViewer to Suspicious Threads findings.
- The suspicious-thread PIDs can be mapped back to named processes through the process enumeration output.

## Unresolved Questions / Limitations

- The SHA-256 hash and original file size of the memory image are not present in the supplied VolViewer reports.
- The Malfind/Suspicious Threads results indicate anomalies but do not independently prove malicious code execution.
- No populated network connection data was available from the supplied Network Scan and Network Status exports.
- Registry hive presence was established, but registry values and persistence locations were not analysed in the supplied export.
- The evidence does not establish the identity or intent of the user who executed `mdd_1.3.exe`.

## Category Conclusion

The memory examination establishes a Windows XP SP3 system with a documented process and thread environment and several memory anomalies flagged by VolViewer. The strongest areas requiring further examination are the Malfind/Suspicious Threads findings and the context surrounding `hkemd.exe`, `cmd.exe`, and `mdd_1.3.exe`. The supplied evidence supports describing these as forensic indicators and correlations rather than making an unsupported definitive attribution of malware or attacker activity.
