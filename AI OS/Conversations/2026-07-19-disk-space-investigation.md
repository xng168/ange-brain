# Disk Space Investigation

- **Problem identified**: ~278 GB of unaccounted storage on C: drive; mapped known locations (Windows: 64 GB, user files: 67 GB, Program Files: 21.6 GB, ProgramData: 21.7 GB, system overhead: 23.1 GB) to only 197 GB total.
- **Root cause diagnosis**: System Restore snapshots likely consuming 100–200+ GB; two additional user accounts (`marti`, `Hatchstone`) on machine are also inaccessible to standard scanning—clarify if they're yours or legacy.
- **Key blocker**: Permission limitations prevent direct scanning of System Volume Information and other user profiles; solution requires running Windows Disk Cleanup tool with admin elevation.
- **Recommended next step**: Use Windows Disk Cleanup (Start → "Disk Cleanup" → "Clean up system files" button → check "System Restore and Shadow Copies") to surface and selectively delete old restore points; single action could free 50–200+ GB.
- **No code/automation done**: This was a diagnostic session; no files modified or scripts written—all findings delivered as actionable manual steps for the user.
