# Security

## What wwt-lite does and does not do

- Runs only on your computer. The engine talks to Chrome over a local pipe, not a network port.
- Uses its own Chrome profile. Your normal Chrome profile, its cookies and its saved passwords are never read or changed.
- Does not read, store or send your passwords, cookies or tokens, and does not solve CAPTCHAs. When a site asks you to sign in or confirm something, the agent can hand the window to you so you do it yourself.
- You can take over any window at any time with **Take over**; the agent pauses until you press **Resume**.
- Installs into your user folder without administrator rights. The installer checks every download against `SHA256SUMS`. macOS builds are signed with an Apple Developer ID and notarized.

## Reporting a vulnerability

Please do not open a public issue for security problems. Use GitHub's **Report a vulnerability** (Security tab of this repository). We aim to reply within 7 days.
