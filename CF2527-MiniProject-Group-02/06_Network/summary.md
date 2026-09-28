# Network / PCAP — Investigation Summary (Evidence File 3)

## Evidence Files Investigated

| File | Analyst | Hash |
|---|---|---|
| `net-2009-11-15-09_24.dmp` | Atharv Nair (PRN 25030241081) | `f35e39a7d8533c07341ce490b9db00a93b5815e9defae87919d85425c9173a92` |

Hash algorithm: SHA-256. Full method and results: [analysis.md](analysis.md). Supporting tables: [A1 Endpoints](appendix/A1_endpoints.md) · [A2 DNS/HTTP/Webmail](appendix/A2_dns_http_webmail.md) · [A3 Reproduction steps](appendix/A3_reproduction_steps.md).

---

## Summary Statistics

- Number of evidence files: 1 (libpcap 2.4, Ethernet)
- Total size: 11,531,810 bytes (about 11.0 MiB)
- Capture window: 2009-11-15 09:24:52 PST to 2009-11-16 09:24:50 PST (about 24 h)
- Number of packets examined: 33,773 (IPv4 29,710 · LLDP 2,869 · ARP 971 · IPv6 223)
- IPv4 endpoints: 85 (more than either other evidence file — driven by active browsing)
- Relevant artefacts identified: 7 (see analysis.md Section 4)
- **Suspicious / high-value artefact: cleartext webmail credentials for 2 users** (`terry`, `pat`)

---

## Top 5 IP Addresses by Packet Count (Statistics → Endpoints → IPv4)

| Rank | IP address | Packets | MAC | Hostname / role |
|---|---|---|---|---|
| 1 | `192.168.1.50` | 10,892 | `00:0f:66:ae:e9:8a` | Unidentified (consistent across all 3 evidence files) |
| 2 | `192.168.1.1` | 10,301 | `00:19:e3:e7:5d:23` | Gateway / DHCP / DNS |
| 3 | `192.168.1.105` | 8,866 | `00:08:74:38:01:b4` | M57-Terry — active browsing this capture |
| 4 | `224.0.0.1` | 2,880 | — | Multicast (not a host) |
| 5 | `192.168.1.103` | 2,740 | `00:0b:db:63:5b:d4` | m57-pat |

Sixth and seventh: `192.168.1.104` (2,267, m57-charlie) and `192.168.1.102` (1,980, m57-jo).

---

## Files / Artefacts Investigated

### 1. ⚠ Cleartext webmail credentials

**Finding:** Terry (`terry`/`UBScfINr`, two logins) and Pat (`pat`/`Hw*JJbJL`, one login) log in to `webmail.m57.biz` over plain HTTP. The username and password are visible in cleartext in the capture. This is a genuine security weakness and a directly usable lead for the Email evidence category.

### 2. Browser keystroke reconstruction (NBNS)

**Finding:** Terry's NetBIOS traffic independently confirms, character by character, that he typed `webmail.m57.biz` and `www.simson.net` into a browser — corroborating Finding 1 from a second, independent data source.

### 3. Endpoint statistics

**Finding:** Top 5 led by the unidentified host `.50`, followed by the gateway, Terry (elevated due to browsing), a multicast address, and Pat.

### 4. Host `192.168.1.50`

**Finding:** Identical traffic signature (fixed source port, TTL 150, DNS/NTP-only) observed for a third time across a third separate capture day. Still unidentified.

### 5. Recurring cross-capture artefacts

**Finding:** Charlie's `explabs.net` machine ID matches all three evidence files; Jo and Pat's unanswered `M57-CHARLIE` NBNS lookups recur from evidence file 2.

---

## Consolidated Findings

1. Two sets of webmail credentials (`terry`/`UBScfINr`, `pat`/`Hw*JJbJL`) were captured in cleartext — the standout finding of this evidence file.
2. Independent NetBIOS evidence confirms the browsing activity behind the credential capture.
3. The Top 5 IPs are led by the still-unidentified `192.168.1.50`, followed by the gateway, an actively browsing Terry, a multicast address, and Pat.
4. `192.168.1.50`'s signature is now confirmed identical across all three network evidence files.
5. Charlie's machine identity and the Jo/Pat → Charlie NBNS lookups both recur, strengthening earlier findings.
6. Aside from the credential weakness, no other evidence of malicious activity was found.

---

## Correlations

- **Email (to confirm, high priority):** try the captured credentials against any `webmail.m57.biz` / `mailboxes.m57.biz` access in the Email evidence.
- **Network-to-network (verified):** Charlie's `explabs.net` machine ID matches across all three network evidence files.
- **Network-to-network (verified):** Jo/Pat's `M57-CHARLIE` NBNS lookups match evidence file 2.
- **Disk (to confirm):** browser history for `webmail.m57.biz` / `www.simson.net` on .105 and .103; any device matching `00:0f:66:ae:e9:8a` / `192.168.1.50`.

---

## Unresolved Questions / Limitations

- Identity of `192.168.1.50` — still unresolved after three evidence files.
- Whether the captured credentials are still valid, or were later changed, cannot be established from this evidence alone.
- Full content of the webmail messages Terry read was not reviewed (out of scope for a network-layer summary).

---

## Category Conclusion

This third evidence file provides the single most actionable finding across all three network captures: two sets of cleartext webmail credentials, independently corroborated by NetBIOS-level keystroke reconstruction. This is a real security weakness (no transport encryption on the login form) and a direct lead for the Email evidence category. The rest of the traffic is consistent with the other two evidence files — ordinary update/security-software communication, a recurring unidentified host, and a recurring unresolved share-connection attempt from Jo and Pat toward Charlie's machine.
