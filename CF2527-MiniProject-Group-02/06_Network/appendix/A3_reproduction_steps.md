# Appendix A3 — Reproduction Steps, Filters and Screenshot Checklist (Evidence File 3)

**Evidence file:** `net-2009-11-15-09_24.dmp`  
**SHA-256:** `f35e39a7d8533c07341ce490b9db00a93b5815e9defae87919d85425c9173a92`  
**MD5:** `fca2c71fbee313bc60cb79bee3e19451`  
**Size:** 11,531,810 bytes

---

## A3.1 Hash verification

```powershell
Get-FileHash -Algorithm SHA256 .\net-2009-11-15-09_24.dmp
```

Expected: `f35e39a7d8533c07341ce490b9db00a93b5815e9defae87919d85425c9173a92`.

---

## A3.2 Screenshot checklist

Take these in Wireshark with the filter bar and status bar visible. Save each with the exact file name shown.

| # | File name | Action / filter | What it must show |
|---|---|---|---|
| **S1** | `01_endpoints_ipv4.png` | Endpoints → IPv4 → untick "Limit to display filter" → sort by **Packets**, descending | Top rows: `.50` (10,892), `.1` (10,301), `.105` (8,866), `224.0.0.1` (2,880), `.103` (2,740) |
| **S2** | `02_endpoints_ethernet.png` | Endpoints → Ethernet | All MACs including `00:0f:66:ae:e9:8a` and `00:08:74:38:01:b4` |
| **S3** | `03_dhcp_hostnames.png` | `dhcp` filter, add Option 12 as a column | m57-jo, m57-pat, m57-charlie, `M57-Terry`; confirm `.50` has none |
| **S4** | `04_host50_dns.png` | `ip.addr == 192.168.1.50 && udp.port == 53`, expand one empty-name packet | Same non-standard pattern as the other two evidence files |
| **S5** | `05_webmail_login_terry.png` | `http.request.uri contains "redirect.php"`, select frame **30386**, Follow → TCP Stream (or expand the raw bytes) | The cleartext `login_username=terry&secretkey=UBScfINr` — **this is the most important screenshot in this evidence file** |
| **S6** | `06_nbns_keystrokes_terry.png` | `nbns && ip.src == 192.168.1.105`, sorted by Time | The incremental `WE` → `WEB` → `WEBM` → … sequence |
| **S7** | `07_nbns_charlie.png` | `nbns && (ip.src == 192.168.1.102 || ip.src == 192.168.1.103) && nbns.name contains "CHARLIE"` | Repeated unanswered `M57-CHARLIE` lookups |
| **S8** | `08_http_requests.png` | Statistics → HTTP → Requests | Full host list, including `webmail.m57.biz` and `i.cdn.turner.com` |
| **S9** | `09_dns_queries.png` | `dns.flags.response == 0` | Note the Displayed count |
| **S10** | `10_capture_properties.png` | Statistics → Capture File Properties | 33,773 packets, SHA-256 hash |

**Optional, if time allows:**
- `http.request.uri contains "redirect.php"` filtered to frame **33588** — Pat's login, for a second confirmed credential capture
- `dns.flags.rcode == 3` — the `_ldap._tcp.dc._msdcs.m57.biz` NXDOMAIN (Active Directory lookup failure)
- Conversations → IPv4, sorted by Bytes — to see Terry's browsing volume relative to the others

---

## A3.3 A note on the credentials screenshot (S5)

This is the one screenshot in this evidence file that carries real weight — everything else here can be reasonably inferred without a screenshot, but a plaintext credential capture needs to be shown, not just described. When you take it:

1. Filter `http.request.uri contains "redirect.php"`.
2. Click on frame **30386** (Terry's second packet — the one carrying the form body, not just the headers).
3. In the bytes pane, make sure `login_username=terry&secretkey=UBScfINr` is visible and highlighted (Wireshark usually highlights it automatically if you click the "HTML Form URL Encoded" line in the detail pane).
4. Take the screenshot with the filter bar, the packet list, and the highlighted bytes all visible.

---

## A3.4 Tools and resources used

| Tool / resource | Purpose |
|---|---|
| Wireshark | Primary analysis tool |
| Python 3 with `dpkt` | Independent scripted cross-check of counts and decoded fields |
| Claude (Anthropic LLM) | Assisted with artefact interpretation, report structuring and cross-check scripting; all statements — including the credential capture — should be re-verified against the capture in Wireshark before submission |

> AI-generated statements are not evidence. Verify the credential values (S5) and the host-.50 traffic (S4) yourself before relying on them.
