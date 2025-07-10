**README: ARP Spoofing Case Study (IOC 23)**

**Project Title: ARP Spoofing via Wi-Fi Breach (Man-in-the-Middle Attack)**

**Objective:**

Simulate and analyze an ARP spoofing attack originating from a Wi-Fi breach.

Identify unsolicited ARP replies in packet captures.

Triangulate evidence across Wireshark, NetFlow, and switch logs.

Align the attack sequence and triage response with the Cybersecurity Battlefield model.

**Attacker Behavior:**

Attacker joined internal network via compromised Wi-Fi.

Sent repeated unsolicited ARP replies to poison ARP caches.

Claimed default gateway IP, diverting local traffic through attacker's MAC.

Operated at OSI Layer 2 to become a man-in-the-middle.

**Telemetry Observed:**

Wireshark captured gratuitous ARP replies.

MAC address mismatch: Attacker MAC claiming to be 192.168.1.1 (gateway).

Frame analysis confirmed spoofed ARP structure.

Switch logs revealed frequent ARP updates for gateway IP.

**Cybersecurity Battlefield Layer Mapping:**

Layer 6: Network Communication — Impact felt by host as routing issues or traffic loss.

Layer 2: Data Link — Primary manipulation layer (ARP cache poisoning).

Layer 4: Credentials & Secrets — Potential pivot if attacker captures session credentials.

**Host OS Interaction:**

Host unaware unless escalated (e.g., credentials stolen).

Possible Layer 6 to Layer 4 pivot: stolen session tokens.

ARP spoofing creates indirect symptoms, not logged locally.

**OSI Layer Mapping:**

Layer 2: ARP reply injection

Layer 3: IP packet misrouting

Layer 7: Potential application-layer compromise (e.g., email, web sessions)

**Triage Methodology:**

Wireshark: Detect unsolicited ARP replies from unrecognized MACs.

Switch Logs: Verify frequent ARP updates to gateway IP.

NetFlow: Monitor for abnormal traffic paths and sudden rerouting.

Firewall Logs: Detect duplicate MACs or unusual ARP broadcast volume.

**Tools Used:**

Wireshark

TCPDump

Switch CLI / Management Console

NetFlow (simulated analysis)

**Defender Actions:**

Detected spoofed ARP packets and MAC/IP mismatches.

Validated affected endpoints' ARP caches.

Enabled Dynamic ARP Inspection (DAI) and port security.

Isolated spoofing device via MAC traceback.

Added ARP watch and anomaly alerts to SIEM.

**Lessons Learned:**

ARP spoofing remains highly effective in flat networks.

Lack of DAI or port-level protections creates blind spots.

Cross-layer understanding is essential to trace escalation paths.

Packet capture is a vital tool for initial detection.

**Cybersecurity Battlefield Relevance:**

This case study reinforces the need for network-layer defenses and cross-layer pivot awareness.

Emphasizes strong telemetry and responsive triage aligned with battlefield layers.

Illustrates adversary tactics that exploit trust in local addressing protocols.

