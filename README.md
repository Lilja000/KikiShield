# KikiShield

Made By Kiki #72385

Standalone protection addon for Bondage Club R132.

**[Install KikiShield 0.6.1](https://raw.githubusercontent.com/Lilja000/KikiShield/main/KikiShield.user.js)**

Open the link with Tampermonkey enabled, confirm installation, and reload the game. Keep only one enabled KikiShield copy.

- Incoming BCC isolation is on by default. LSCG isolation is optional and off by default.
- Equal icon tabs for Protection, Automation and Activity, aligned setting rows and matching controls. A fixed-size panel with a scrolling body keeps navigation in place and adapts to smaller viewports.
- A red launcher badge counts new Activity events and clears when you view Activity.
- Native permission, blacklist and ghost checks for supported incoming actions.
- Panic mode hides the game, filters new messages and mutes supported audio without leaving the server.
- Expand an Activity event to see its command, target, blocking reason, severity and retained payload. Severity describes evidence, not a person's intent.
- Optional automatic blacklist or ghost actions for serious blocked attempts or observed BCC/LSCG traffic. Automation is off by default; trusted people are excluded by default. BC ghosting also blacklists.
- Read [README.txt](README.txt), [VERIFICATION.txt](VERIFICATION.txt) and [BCC-Audit.html](BCC-Audit.html) for scope, test coverage and limitations.

Activity stays in memory in this tab. Retained command arguments may contain private content; review exports before sharing. Ordinary chat and Panic text are not retained. Payloads are capped at 64 KiB per event and 1 MiB across at most 100 records.

This is a client-side shield. It cannot prevent another client from copying appearance data already visible to it, and cannot guarantee compatibility with every addon.
