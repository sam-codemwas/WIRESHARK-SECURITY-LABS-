# ARP Packet Analysis — Investigation Report

**Project:** 01 — ARP Packet Analysis  
**Category:** Network Traffic Analysis  
**Tool:** Wireshark  
**Operating System:** Windows  
**Dataset:** arp-storm.pcap  

---

## 1. Summary

This investigation examines Address Resolution Protocol (ARP) traffic using Wireshark to understand how devices resolve IPv4 addresses into physical MAC addresses.

The analysis identified repeated ARP request-and-reply exchanges between two devices on the `192.168.100.0/24` network.

A device using IP address `192.168.100.1` requested the MAC address associated with `192.168.100.19`. The responding device successfully supplied its MAC address.

Repeated ARP communication was observed in the packet capture, warranting further examination of network behaviour.

No definitive evidence of ARP spoofing or malicious activity can be established from the screenshot alone.

## 2. Investigation Objectives

- Understand ARP communication.
- Identify ARP requests and replies.
- Examine sender and target IP addresses.
- Identify associated MAC addresses.
- Investigate repeated ARP communication.
- Assess whether observed behaviour requires further security investigation.

## 3. Lab Environment

| Component | Description |
|---|---|
| Operating System | Windows |
| Analysis Tool | Wireshark |
| Protocol | ARP |
| Dataset | arp-storm.pcap |
| Environment | Offline PCAP analysis |

## 4. Investigation Methodology

The following steps were performed:

1. Opened the supplied ARP PCAP file in Wireshark.
2. Applied the `arp` display filter.
3. Examined ARP requests using `arp.opcode == 1`.
4. Examined ARP replies using `arp.opcode == 2`.
5. Selected an ARP reply packet for detailed examination.
6. Expanded the Address Resolution Protocol section.
7. Recorded sender and target IP and MAC addresses.
8. Examined repeated ARP communication in the packet list.

## 5. Evidence and Packet Observations

### 5.1 ARP Request

The packet list displayed the following request:

`Who has 192.168.100.19? Tell 192.168.100.1`

This indicates that the device at `192.168.100.1` was requesting the MAC address associated with `192.168.100.19`.

### 5.2 ARP Reply

The corresponding response displayed:

`192.168.100.19 is at 4c:44:5b:a8:53:63`

The selected packet was Frame 12.

### 5.3 Extracted Packet Details

| Field | Observed Value |
|---|---|
| Frame Number | 12 |
| Protocol | ARP |
| Opcode | Reply (2) |
| Hardware Type | Ethernet (1) |
| Protocol Type | IPv4 (0x0800) |
| Hardware Size | 6 |
| Protocol Size | 4 |
| Sender IP | 192.168.100.19 |
| Sender MAC | 4c:44:5b:a8:53:63 |
| Target IP | 192.168.100.1 |
| Target MAC | fc:18:03:81:eb:bf |
| Frame Length | 42 bytes |

### 5.4 Repeated ARP Communication

Multiple request-and-reply exchanges involving the same IP addresses were visible.

Examples included packets 11–14 and 930–933.

This indicates repeated address-resolution activity involving the same devices.

The exact total number of ARP packets and the frequency of these exchanges require examination of the complete capture.

## 6. Security Analysis

Repeated ARP communication can occur under normal network conditions.

However, excessive or unexpected ARP activity may warrant investigation for:

- Unusual address-resolution behaviour.
- Possible ARP spoofing.
- Duplicate IP address conflicts.
- Unexpected changes in IP-to-MAC mappings.

The available evidence establishes repeated ARP communication but does not independently demonstrate malicious activity.

Additional evidence would be required before classifying this activity as suspicious or malicious.

## 7. Recommendations

- Monitor unexpected changes in IP-to-MAC address mappings.
- Investigate unusually frequent ARP requests.
- Maintain network visibility through appropriate monitoring tools.
- Consider Dynamic ARP Inspection where supported by network infrastructure.
- Correlate ARP observations with other network and endpoint security logs.

## 8. Conclusion

The investigation successfully demonstrated how ARP requests and replies facilitate IPv4-to-MAC address resolution.

Wireshark was used to identify the communicating devices and extract relevant network information.

Repeated ARP exchanges involving `192.168.100.1` and `192.168.100.19` were observed.

The exercise provided practical experience in packet inspection, protocol identification, evidence collection, and basic network security analysis.

Further investigation of the complete capture is recommended before drawing conclusions about potential network threats.

## 9. Tools and References

- Wireshark: https://www.wireshark.org/
- Wireshark Documentation: https://www.wireshark.org/docs/
- Wireshark Sample Captures: https://wiki.wireshark.org/SampleCaptures
