# Disk Space & npm/Expo App Troubleshooting Session

- **Problem diagnosed**: Only 397 MB free disk space on C:\ — npm and Expo can't install/bundle without elbow room for temp files; ngrok install previously failed due to this constraint
- **Root cause identified**: System Restore and Shadow Copies likely consuming ~278 GB (needs explicit cleanup via "Clean up system files" in Disk Cleanup utility)
- **Action items for next session**:
  1. Run Disk Cleanup → "Clean up system files" → select "System Restore and Shadow Copies" → delete
  2. Target: free at least a few GB to enable npm/Expo to function safely
  3. Once complete: retry `npx expo start --tunnel` to test app on iPhone
- **Blocker**: This disk space issue is blocking app testing and progress on M6 (parent area); cleanup is the critical unblock before continuing development work
