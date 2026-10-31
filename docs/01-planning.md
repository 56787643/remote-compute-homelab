# 01 - Planning

## Goal
Use a ThinkPad X240 as a thin client that harnesses a desktop PC's compute remotely, with an isolated security lab and a small NAS, while keeping electricity costs low.

## Hardware
- **Host PC:** Intel i5-11400F, 16 GB RAM, GTX 1650, SATA SSDs plus a 2 TB 7200 RPM HDD, Windows 10 IoT Enterprise LTSC
- **Client:** ThinkPad X240, i5-4300U, 8 GB RAM, 128 GB SSD, Linux Mint

## Use cases
- Terminal and scripting work, CTF tooling, VMs (primary)
- Occasional graphical apps such as photo editing and Wireshark
- Gaming is out of scope for now, but the same stack would support it later

## Options considered
| Need | Options | Decision | Reason |
|---|---|---|---|
| Remote access | Port forwarding, WireGuard, Tailscale | Tailscale | No exposed ports, works behind CGNAT, simple key management |
| Dev work | RDP, streaming, SSH | SSH + VS Code Remote | Lightest, works on weak clients |
| Graphical access | RDP, Parsec, Sunshine/Moonlight | Sunshine + Moonlight | GPU hardware encoding, low latency, no cloud account |
| Waking the PC | Wake-on-LAN, smart plug, always-on | WoL at home, smart plug away | Avoids running the PC 24/7 |

## Threat model
**Assets:** personal files, the PC itself, credentials, the identity account that controls the private network.

**Likely threats and mitigations:**
| Threat | Mitigation |
|---|---|
| Internet scanning for exposed services | No ports forwarded; all access through Tailscale |
| SSH brute force | Key-only authentication, password auth disabled |
| Compromised identity account | 2FA on the Tailscale login account |
| Malware or exploit practice affecting real data | Lab VMs on isolated networks, no shared folders, no access to NAS data |
| Data loss | Multiple copies, offsite copy, tested restores |

## Known weaknesses (identified before building)
- Remote wake-up is fragile; power cuts or router reboots can lock me out
- Single points of failure: one PC, one ISP, one router
- NAS on one disk has no redundancy; backups are separate and required
- 16 GB RAM limits how many lab VMs run at once
- Streaming adds latency and compression artifacts

## Power cost estimate (to be replaced with measurements)
| Device | Estimated idle | Notes |
|---|---|---|
| ThinkPad X240 | about 7 W | Not required to stay on |
| Desktop PC | about 35-50 W | Dedicated GPU is required because the CPU has no integrated graphics |

Plan: measure real idle draw with a smart plug that has a watt meter, then decide between always-on and on-demand.

## Success criteria
- Open a folder on the PC from the laptop over SSH
- Use a graphical app on the PC from the laptop with a smooth stream
- Wake the PC remotely
- Lab VMs cannot reach the NAS data
- Documented measurements for latency, bandwidth and power
