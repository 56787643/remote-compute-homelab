# Decisions and mistakes

A running log of choices I made, things I got wrong, and what changed my mind.

## 1. Skipping the Windows 11 upgrade
- **Plan:** upgrade the host from Windows 10 to Windows 11 via a clean install.
- **Finding:** `msinfo32` showed the OS is Windows 10 IoT Enterprise LTSC, which receives security updates for years, so the usual "Windows 10 is end of life" urgency does not apply. A clean install would also have replaced it with a regular edition needing a separate license.
- **Decision:** keep the current OS and skip the BIOS mode change and wipe.
- **Lesson:** check what you actually have before planning a migration.

## 2. Backup method
- **Plan:** use Google Drive for desktop in backup mode.
- **Finding:** that option is no longer offered for folders; only two-way sync is available, which deletes cloud copies when local files are deleted.
- **Decision:** one-time upload through the web interface instead, then verify by opening files and comparing counts.
- **Lesson:** documentation and tutorials go out of date; read what the tool actually offers.

## 3. VPN interference on the speed test
- **Finding:** the first speed test ran through a VPN client and showed very high latency under load.
- **Decision:** re-test with it off and keep it off while Tailscale is in use.
- **Lesson:** change one variable at a time when measuring.

## Open questions
- Real idle power draw of the host
- Whether the Tailscale connection is direct or relayed on this ISP
