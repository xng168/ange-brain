# Expo Go & VPN Connectivity Debugging

- **Problem identified**: Astrill VPN's virtual network adapter was interfering with Expo Go's ability to scan QR codes from the phone, even after disconnecting the VPN
- **Root cause found**: VPN adapter remained "Up" in Windows networking despite traffic stopping, still blocking connectivity
- **Solution approach**: Fully terminate the Astrill VPN app (not just disconnect), force-close Expo Go, and rescan QR code
- **Next action**: Need screenshot of current error state after completing above steps to continue diagnosis
- **Status**: Waiting on user execution of troubleshooting steps; session paused pending error feedback
