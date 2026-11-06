# ARP Packet Analysis — Findings and Observations

## 1.Findings

The investigation examined Address Resolution Protocol (ARP) traffic using Wireshark to understand how devices identify each other through IPv4 and MAC address mapping.

The supplied `arp-storm.pcap` capture was filtered using the `arp` display filter to isolate ARP communication.

## 2. ARP Requests Observed

The packet list revealed repeated ARP requests containing the following message:

`Who has 192.168.100.19? Tell 192.168.100.1`

This indicates that the device with IP address `192.168.100.1` was requesting the MAC address associated with `192.168.100.19`.

## 3. ARP Replies Observed

A corresponding ARP reply was identified in Frame 12:

`192.168.100.19 is at 4c:44:5b:a9:53:64`

The packet details provided the following information:

| Attribute | Observation |
|---|---|
| Frame Number | 12 |
| Protocol | ARP |
| Opcode | Reply (2) |
| Sender IP | 192.168.100.19 |
| Sender MAC | 4c:44:5b:a4:53:66 |
| Target IP | 192.168.100.1 |
| Target MAC | fc:18:03:81:eb:bf |
| Hardware Type | Ethernet (1) |
| Protocol Type | IPv4 (0x0800) |
| Packet Length | 42 bytes |

## 4. Repeated ARP Activity

Multiple ARP request-and-reply exchanges involving the same two IP addresses were visible in the packet list.

Examples included:

- Frames 11–14.
- Frames 930–933.
- Additional repeated exchanges later in the capture.

This demonstrates recurring address-resolution activity between the identified devices.

The complete packet count and exact frequency of these exchanges have not yet been established.

## 5. Key Technical Observations

1. The capture contains both ARP requests and replies.
2. The device at `192.168.100.1` requested the MAC address of `192.168.100.19`.
3. The responding device identified its MAC address as `4c:44:5b:a8:53:63`.
4. The ARP reply contained the expected Ethernet and IPv4 protocol information.
5. Repeated address-resolution exchanges were visible throughout the displayed packet list.

## 6. Security Observations

Repeated ARP requests may occur during normal network operations. However, unusual ARP frequency or unexpected IP-to-MAC address changes can warrant further investigation.

The observed traffic provides a reason to examine the complete capture for:

- Unexpected ARP frequency.
- Inconsistent IP-to-MAC mappings.
- Duplicate IP address behaviour.
- Potential ARP spoofing indicators.

No confirmed malicious activity can be established from the currently examined packets.

## 7. Conclusion

The investigation successfully identified ARP request-and-reply communication and extracted relevant IP and MAC address information.

The exercise demonstrated how Wireshark can be used to inspect network protocols, examine packet details, and identify recurring communication patterns.

The findings establish normal ARP resolution behaviour in the examined exchange, while repeated activity remains an area for further investigation.
