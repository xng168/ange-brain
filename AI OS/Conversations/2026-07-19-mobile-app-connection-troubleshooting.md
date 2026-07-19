# Mobile App Connection Troubleshooting

• **Identified disk space issue** – Fixed a critical storage constraint on the PC that was likely causing connection failures and cascading errors

• **Diagnosed ngrok tunnel flakiness** – Recognized that "URL generated but nothing connects" is a known free-tier ngrok reliability problem, not a misconfiguration in the app setup

• **Key decision: simplify first** – After disk space fix, decided to test with plain `npm start` (no tunnel) before pursuing complex workarounds, since earlier failures may have been side effects of the storage problem

• **Windows Firewall identified as likely culprit** – Flagged that an early Windows Security popup asking to allow network access may have been dismissed, potentially blocking the first connection attempt on the PC

• **Next steps**: Check terminal state, run `npm start`, watch for Firewall popup (allow both Private/Public networks), rescan iPhone QR code
