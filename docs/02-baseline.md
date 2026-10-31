# 02 - Network baseline

## Goal
Know the real limits of the home connection before choosing streaming settings.

## Method
Browser-based speed test run from the host PC, once with a VPN client active and once without.

## Results
| Metric | With VPN client active | Without VPN client |
|---|---|---|
| Download | about 36 Mbps | about 54 Mbps |
| Upload | about 53 Mbps | about 64 Mbps |
| Idle latency | 7 ms | 9 ms |
| Latency under download load | 75 ms | 28 ms |
| Latency under upload load | 227 ms | 67 ms |
| Jitter | not measured | about 5 ms |
| Packet loss | not measured | 0% |

## What this showed
- The VPN client added a large amount of latency under load, so most of the "bufferbloat" first observed came from it, not from the line itself.
- Upload of about 64 Mbps is roughly 3x what a 1080p60 stream needs (about 15-20 Mbps), so bandwidth is not the bottleneck.
- Download is capped well below the advertised line speed by the home router, which matters for large downloads but not for streaming.
- Loaded latency of about 67 ms on upload is acceptable, but a stream should be capped around 15 Mbps so it does not saturate the link.

## Decisions that follow
- Keep other VPN clients off while using Tailscale to avoid routing and DNS conflicts
- Cap the stream bitrate at about 15 Mbps
- Schedule large uploads and backups outside streaming sessions

## Notes
Screenshots of speed tests show the public IP and ISP; crop them before committing.
